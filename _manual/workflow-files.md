---
layout: manual
title: "Workflow Files"
description: "What Mainline expects from your GitHub Actions workflow YAML — required triggers, runner image, and the build → sign → upload step shape."
breadcrumb: true
permalink: /manual/workflow-files/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Workflow Files</h1>
  <p>What Mainline expects in your <code>.github/workflows/</code> YAML — and what you can leave alone.</p>
</div>

## Overview

Mainline doesn't generate or own your workflow YAML — your CI pipeline stays under your control. But Mainline's CI features (Trigger Build, secret injection, live run monitoring) have a few baseline assumptions about how the workflow is shaped. This page lays them out.

If you don't have a workflow yet, the [test_app](https://github.com/meshterm-testing/test_app/blob/main/.github/workflows/testflight.yml) and [sandbox](https://github.com/meshterm-testing/sandbox/blob/main/.github/workflows/testflight.yml) repositories used by Mainline's own App Review process are good copy-paste starting points.

---

## Required structure

A workflow that Mainline can drive end-to-end has four parts:

<ol class="steps">
  <li><strong>A push trigger</strong> on the branch you ship from (typically <code>main</code>).</li>
  <li><strong>A macOS runner</strong> with the iOS SDK you build against — currently <code>macos-26</code> for iOS 26.</li>
  <li><strong>A signing step</strong> that imports a P12 from secrets into a temporary keychain.</li>
  <li><strong>An upload step</strong> that calls <code>xcrun altool --upload-app</code> with App Store Connect API credentials.</li>
</ol>

A minimal example:

```yaml
name: Build & Deploy to TestFlight

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: macos-26
    timeout-minutes: 12
    steps:
      - uses: actions/checkout@v4

      - name: Install certificate
        env:
          P12_BASE64: ${{ secrets.CERTIFICATE_P12_BASE64 }}
          P12_PASSWORD: ${{ secrets.P12_PASSWORD }}
        run: |
          echo "$P12_BASE64" | base64 --decode > /tmp/certificate.p12
          security create-keychain -p "" build.keychain
          security import /tmp/certificate.p12 -k build.keychain \
            -P "$P12_PASSWORD" -T /usr/bin/codesign -f pkcs12
          security list-keychains -s build.keychain
          security default-keychain -s build.keychain
          security unlock-keychain -p "" build.keychain
          security set-key-partition-list -S apple-tool:,apple: \
            -s -k "" build.keychain

      - name: Install provisioning profile
        env:
          PROFILE_BASE64: ${{ secrets.APP_PROFILE_BASE64 }}
        run: |
          mkdir -p ~/Library/MobileDevice/Provisioning\ Profiles
          echo "$PROFILE_BASE64" | base64 --decode > \
            ~/Library/MobileDevice/Provisioning\ Profiles/app.mobileprovision

      - name: Build archive
        run: |
          xcodebuild -scheme MyApp \
            -configuration Release \
            -archivePath /tmp/MyApp.xcarchive \
            -destination "generic/platform=iOS" \
            -sdk iphoneos \
            CODE_SIGN_STYLE=Manual \
            CURRENT_PROJECT_VERSION=$GITHUB_RUN_NUMBER \
            archive

      - name: Export IPA
        run: |
          xcodebuild -exportArchive \
            -archivePath /tmp/MyApp.xcarchive \
            -exportPath /tmp/MyApp-Export \
            -exportOptionsPlist ExportOptions.plist

      - name: Upload to TestFlight
        if: ${{ !contains(github.event.head_commit.message, '[skip upload]') }}
        env:
          ASC_KEY_ID: ${{ secrets.APP_STORE_CONNECT_API_KEY_KEY_ID }}
          ASC_ISSUER_ID: ${{ secrets.APP_STORE_CONNECT_API_KEY_ISSUER_ID }}
          ASC_KEY_CONTENT_BASE64: ${{ secrets.APP_STORE_CONNECT_API_KEY_KEY }}
        run: |
          mkdir -p ~/.appstoreconnect/private_keys
          echo "$ASC_KEY_CONTENT_BASE64" | base64 --decode > \
            ~/.appstoreconnect/private_keys/AuthKey_${ASC_KEY_ID}.p8
          xcrun altool --upload-app \
            --type ios \
            --file /tmp/MyApp-Export/MyApp.ipa \
            --apiKey "$ASC_KEY_ID" \
            --apiIssuer "$ASC_ISSUER_ID"
```

See [Secrets naming]({{ '/manual/secrets-naming/' | relative_url }}) for what each `secrets.*` reference means and how Mainline maps to whichever names your team prefers.

---

## You don't need `workflow_dispatch:`

Earlier versions of Mainline required workflows to declare `on: workflow_dispatch:` so the Trigger Build button could fire them. **That's no longer the case.** Mainline now triggers builds by either re-running the last completed run (clean) or pushing an empty commit (fallback). Both work against any workflow that has ever fired on push.

If you'd like manual dispatch wired into the workflow itself anyway — for example to run from GitHub's web UI — adding `workflow_dispatch:` is fine, but Mainline doesn't depend on it.

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Why no <code>workflow_dispatch</code>?</div>
    <p>
      The dispatch endpoint requires the workflow to opt in, and surfaces an unactionable 422 error when it doesn't. Falling back to "rerun or empty commit" works regardless and avoids ever editing your workflow file under you.
    </p>
  </div>
</div>

---

## The `[skip upload]` marker

When you push commits that compile-test something but you don't want to consume a TestFlight upload slot — for example, when you're iterating on workflow YAML itself — include `[skip upload]` anywhere in the commit message. The `if:` clause on the upload step skips altool while still building and signing.

```bash
git commit -m "ci: fix indentation in build step [skip upload]"
```

Two things to watch:

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">The marker matches the commit body too</div>
    <p>
      GitHub Actions' <code>contains()</code> check matches the entire <code>head_commit.message</code>, including the body. If you describe a previous skip-upload commit in a later commit's body, that later commit will <em>also</em> skip upload. Avoid quoting the literal phrase in commit messages that you do want to upload.
    </p>
  </div>
</div>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Don't pre-test compile then ship empty</div>
    <p>
      It's tempting to push <code>[skip upload]</code> first to verify the build, then push an empty commit to actually upload. That doubles your runner minutes for no gain — failed builds skip altool anyway. Push the real commit once and read the upload log if you need to verify.
    </p>
  </div>
</div>

---

## Build numbers and `CURRENT_PROJECT_VERSION`

Mainline expects each new TestFlight build to have a higher `CFBundleVersion` than the previous one. The simplest way to achieve this is to pass `CURRENT_PROJECT_VERSION=$GITHUB_RUN_NUMBER` to `xcodebuild archive` — GitHub increments the run number on every workflow run, including reruns and empty-commit triggers, so build numbers stay monotonic without you tracking them.

If you set the build number elsewhere (a `Configuration` file, a script, etc.), make sure that source still produces a strictly increasing value across reruns.

---

## Single-source app icons

If you supply a single 1024×1024 master icon in an `AppIcon.appiconset` (the modern "Single-Size App Icons" feature, supported in Xcode 14+), three things must be in place or App Store Connect rejects the upload:

1. The asset catalog has `idiom: universal, platform: ios` and one 1024×1024 PNG.
2. The build setting `ASSETCATALOG_COMPILER_APPICON_NAME = AppIcon` is set on the target.
3. Info.plist contains `CFBundleIconName = AppIcon`.

If you generate your project with XcodeGen, put the directory containing your `.xcassets` under the target's `sources:` list, **not** `resources:` — the latter creates a folder reference that bypasses `actool` and produces a bundle with no compiled icons of any size.

---

## What Mainline doesn't touch

Mainline doesn't write, edit, or generate workflow YAML. The pipeline is yours. If something breaks at the YAML level — a typo in `on:`, an env var name change, a new Xcode action that needs configuring — that's a manual fix in the file.

The narrow exception is [Secret Injection]({{ '/manual/secret-injection/' | relative_url }}), which writes secret <em>values</em> to GitHub Actions but never modifies the workflow file's references to them.
