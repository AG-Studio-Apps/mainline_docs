---
layout: manual
title: "Secrets Naming Conventions"
description: "The standard GitHub Actions secret names Mainline injects into, and how to adapt to whatever names your existing workflows already use."
breadcrumb: true
permalink: /manual/secrets-naming/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Secrets Naming Conventions</h1>
  <p>The names Mainline writes secrets to — and how to adapt when your workflows expect different ones.</p>
</div>

## The default schema

When Mainline injects code-signing and ASC credentials into a GitHub repository's Actions secrets, it uses these names by default:

| Secret slot | Default name | What it holds |
|---|---|---|
| Distribution P12 | `CERTIFICATE_P12_BASE64` | Base64-encoded PKCS#12 distribution cert + private key |
| P12 password | `P12_PASSWORD` | The P12's inner password (empty string is valid) |
| App Store provisioning profile | `APP_PROFILE_BASE64` | Base64-encoded `.mobileprovision` for the app target |
| Widget extension profile *(optional)* | `WIDGET_PROFILE_BASE64` | Base64-encoded `.mobileprovision` for a widget extension |
| Share extension profile *(optional)* | `SHARE_PROFILE_BASE64` | Base64-encoded `.mobileprovision` for a share extension |
| ASC API key (private key) | `APP_STORE_CONNECT_API_KEY_KEY` | Base64-encoded `.p8` |
| ASC API key ID | `APP_STORE_CONNECT_API_KEY_KEY_ID` | The 10-character key ID |
| ASC API key issuer ID | `APP_STORE_CONNECT_API_KEY_ISSUER_ID` | The team's issuer UUID |

These names match what the [test_app](https://github.com/meshterm-testing/test_app) reference workflow consumes, so a fresh project that copies that workflow needs no schema customisation.

---

## Per-app Secret Schema

Many existing workflows use different names — `MATCH_PASSWORD`, `IOS_CERT_BASE64`, `ASC_KEY_ID`, etc. Rewriting your workflow to match Mainline's defaults isn't necessary, and isn't recommended — your workflow file is yours, and rewriting it is the kind of churn that creates merge conflicts and breaks rollback.

Instead, Mainline keeps a per-app **Secret Schema** that maps each slot to whatever name your workflow already expects. The schema lives on the app record, so different apps in your portfolio can use different conventions side by side.

### Editing the schema

<ol class="steps">
  <li>Open the App Detail view.</li>
  <li>Tap <strong>Secrets → Edit Schema</strong>.</li>
  <li>For each slot, enter the secret name your workflow reads. For example, if your workflow has <code>${{ secrets.IOS_DIST_CERT }}</code>, set the P12 slot to <code>IOS_DIST_CERT</code>.</li>
  <li>Save. Future injections write to those names; injections from before the schema change aren't retroactively renamed.</li>
</ol>

### Auto-detection

If your workflow already exists and is using the secrets it needs, Mainline can read the YAML and infer the schema:

<ol class="steps">
  <li>In the Secret Schema editor, tap <strong>Detect from Workflows</strong>.</li>
  <li>Mainline scans <code>.github/workflows/*.yml</code> for <code>${{ secrets.X }}</code> references and proposes a mapping based on the names it recognises (and on conventional naming heuristics like <code>*_P12_*</code>, <code>*PROFILE*</code>, <code>ASC_*</code>).</li>
  <li>Review the proposed mapping, adjust any uncertain slots, and save.</li>
</ol>

This is the recommended path for apps you're onboarding to Mainline that already have working CI — it's faster than retyping names and less error-prone than copy-paste.

---

## .p8 encoding

ASC API keys are issued as `.p8` PEM files. Some workflows expect the raw PEM contents in the secret, others expect base64-encoded bytes. Mainline's schema editor has a per-app toggle for this — choose what your workflow's `Upload to TestFlight` step expects, and Mainline writes the value in the matching encoding.

If you're authoring a fresh workflow, the base64-encoded form is slightly more robust because it survives any newline-stripping that GitHub Actions might apply to the secret value during decoding.

---

## Optional vs. required slots

Not every workflow needs every slot. The Secret Schema editor marks each slot as required or optional:

- **Required** for any TestFlight-uploading workflow: P12, P12 password, app profile, ASC API key + key ID + issuer ID.
- **Optional** depending on your app: widget profile, share extension profile, additional per-target profiles.

Mainline only writes the slots you've populated; unused slots stay absent from the GitHub repo, so you don't end up with empty `WIDGET_PROFILE_BASE64` secrets cluttering the list.

---

## What if a secret already exists with the right name?

If a secret with the same name already exists in the repo, Mainline overwrites it on injection — it's an idempotent write rather than a "create only if missing." This is intentional: the most common reason to inject is to refresh a rotated cert or profile, and refusing to overwrite would defeat the purpose.

The Secrets Setup sheet shows the current state of each slot (Present in GitHub / Missing / Stale) so you know what's about to change before you tap Inject.

---

## Common pitfalls

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Watch for typos in workflow YAML</div>
    <p>
      GitHub Actions silently treats an undefined secret as the empty string — there's no "secret not found" error. If your workflow has <code>${{ secrets.CERFIFICATE_P12_BASE64 }}</code> (note the typo), the cert step will run with an empty input and fail at <code>security import</code> with a confusing error. Auto-detect catches most of these because the proposed mapping won't have an obvious slot for the misspelled name.
    </p>
  </div>
</div>

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Profile names per target, not per app</div>
    <p>
      If your app has multiple targets that need separately-signed profiles (widget, share extension, watch app), each needs its own slot in the schema. Mainline's defaults cover app + widget + share; for additional targets, add custom slots in the schema editor.
    </p>
  </div>
</div>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">When in doubt, copy the test_app workflow</div>
    <p>
      The <a href="https://github.com/meshterm-testing/test_app/blob/main/.github/workflows/testflight.yml">test_app workflow</a> uses Mainline's default secret names verbatim. If you're starting fresh, copying its <code>env:</code> blocks gives you a known-good naming baseline.
    </p>
  </div>
</div>
