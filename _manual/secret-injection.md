---
layout: manual
title: "Secret Injection for CI"
description: "How Mainline writes code-signing secrets to GitHub Actions so your CI pipeline can build and sign."
breadcrumb: true
permalink: /mainline_docs/manual/secret-injection/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Secret Injection for CI</h1>
  <p>Write signing credentials to GitHub Actions secrets so your pipelines can build and sign without a Mac.</p>
</div>

## Overview

For CI builds to sign your app, your GitHub Actions workflows need access to:

- A distribution certificate (as a base64-encoded P12)
- A provisioning profile (as a base64-encoded `.mobileprovision`)
- The P12 password (if encrypted)
- Your ASC API key details (for uploading builds with `altool` or `xcrun notarytool`)

Mainline's **Secret Injection** feature automates writing these to your GitHub repository's Actions secrets — no manual copy-paste of base64 strings.

---

## Setting up secret injection

<ol class="steps">
  <li>Open the App Detail view and tap <strong>Secrets</strong> (shown in the repository section — requires a GitHub PAT and cert repo to be configured).</li>
  <li>Mainline shows a list of the secrets it can inject for this app, with a status indicator for each (present in GitHub, missing, or stale).</li>
  <li>Select a certificate and profile to inject.</li>
  <li>Tap <strong>Inject Secrets</strong>. Mainline writes each secret to the GitHub repo's Actions secrets via the GitHub API.</li>
</ol>

---

## What gets written

Mainline writes the following secrets to your GitHub repo (exact names depend on your **Secret Schema**):

| Secret | Content |
|---|---|
| `DISTRIBUTION_CERTIFICATE_P12` | Base64-encoded P12 |
| `DISTRIBUTION_CERTIFICATE_PASSWORD` | P12 password (or empty string for passwordless P12s) |
| `PROVISIONING_PROFILE` | Base64-encoded `.mobileprovision` |
| `ASC_API_KEY_P8` | Base64-encoded `.p8` private key |
| `ASC_KEY_ID` | ASC Key ID |
| `ASC_ISSUER_ID` | ASC Issuer ID |

---

## Secret Schema

Different teams name their GitHub Actions secrets differently. Mainline uses a **Secret Schema** per app to map the above secret types to whatever names your workflows actually expect.

### Editing the Secret Schema

<ol class="steps">
  <li>In the App Detail view, tap <strong>Secrets → Edit Schema</strong>.</li>
  <li>For each secret slot, enter the name your workflow uses (e.g. if your workflow reads <code>${{ secrets.CERT_P12 }}</code>, set the certificate slot to <code>CERT_P12</code>).</li>
  <li>Save. Mainline uses the schema for all future injections for this app.</li>
</ol>

### Auto-detection

Mainline can inspect your workflow YAML files and suggest a schema automatically. Tap **Detect from Workflows** to let Mainline scan the `.github/workflows/` folder and infer the expected secret names.

---

## YAML Mapper (advanced)

For complex setups where the workflow generates a signing configuration file (rather than reading individual secrets), the **YAML Mapper** lets you define how secret values map to entries in a YAML configuration file. This is an advanced feature intended for teams with non-standard CI setups.

---

## Common pitfalls

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Certificate and profile must match</div>
    <p>
      The P12 you inject must contain the same certificate that was used to generate the provisioning profile. If they don't match, signing will fail silently. Mainline helps by showing which certificate serial number is embedded in each profile.
    </p>
  </div>
</div>

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">GitHub secret writes require <code>secrets: write</code> permission</div>
    <p>
      Your GitHub PAT needs permission to write repository secrets. For fine-grained tokens, this is the <em>Secrets (read and write)</em> permission. For classic tokens, the <code>repo</code> scope covers it.
    </p>
  </div>
</div>
