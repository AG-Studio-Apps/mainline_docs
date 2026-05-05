---
layout: manual
title: "Certificates & Profiles"
description: "Renew distribution certificates, regenerate provisioning profiles, and sync signing assets to your device Keychain."
breadcrumb: true
permalink: /manual/certs-profiles/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Certificates &amp; Profiles</h1>
  <p>Renew certs, regenerate profiles, and sync signing assets — without touching your Mac.</p>
</div>

<!-- SCREENSHOT: certs-section -->
<div class="screenshot-placeholder">
  <span class="ph-icon">🔐</span>
  <span class="ph-label">Certificates & profiles section for an app</span>
  <span class="ph-hint"><!-- SCREENSHOT: certs-profiles-section --></span>
</div>

## Where to find it

Certificates and profiles are accessible from two places:

1. **App Detail view** — shows the certificates and profiles relevant to that specific app (matched by bundle ID)
2. **Dashboard health overview** — shows team-wide signing health, with expiry warnings across all certs

---

## Certificates

The certificates section lists your team's distribution certificates. For each certificate you can see:

- Certificate name and type
- Serial number (last 12 characters shown)
- Expiry date
- Whether it's present in your device Keychain

### Importing a certificate to Keychain

If a certificate is in your cert repo but not in the Keychain, tap **Import from Repo**. Mainline decrypts the P12 from your cert repo and installs it into the iOS Keychain, making it available for use by CI secret injection.

### Renewing a certificate

<ol class="steps">
  <li>Tap <strong>Renew</strong> on an expiring or expired certificate.</li>
  <li>Mainline generates a new certificate via the ASC API. The new certificate is created in ASC.</li>
  <li>If you have a cert repo configured, Mainline offers to write the new P12 to the repo. The old certificate entry is replaced.</li>
  <li>After renewal, re-generate any profiles that were tied to the old certificate (see below).</li>
</ol>

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Renewing a cert invalidates linked profiles</div>
    <p>
      Provisioning profiles are cryptographically linked to the certificate they were generated with. When you renew a cert, you need to regenerate any profiles that used the old one. Mainline shows a warning and offers to regenerate profiles as part of the renewal flow.
    </p>
  </div>
</div>

### Revoking a certificate

Tap **Revoke** to revoke a certificate in ASC. This is permanent and will break any CI pipelines still using the old cert. Only revoke certs that are compromised or truly no longer needed.

---

## Provisioning profiles

Profiles are listed per app (filtered by bundle ID). Each profile shows:

- Profile name and type (App Store, Ad Hoc, Development)
- Bundle ID
- Expiry date
- Whether the profile is active or expired
- Whether it's present in your device Keychain

### Importing a profile to Keychain

Tap **Import** on any active profile to download it from ASC and store it in the Keychain.

### Regenerating a profile

After renewing a certificate, or if a profile has expired, tap **Regenerate** to create a fresh profile in ASC linked to the current certificate. Mainline then offers to push the new profile to your cert repo and Keychain.

---

## Sync

The **Sync** action (Dashboard toolbar or App Detail header) pulls all distribution certs from the cert repo and all active profiles from ASC into the Keychain in one step. Run this on a new device or after a renewal to get everything up to date.

---

## Bundle IDs and capabilities

Tap **Bundle IDs** in the App Detail view to see all bundle IDs associated with your app (main bundle, extensions, widgets). For each bundle ID you can:

- View and edit associated **capabilities** (push notifications, App Groups, CloudKit, etc.)
- Register a new bundle ID for an extension or widget
- View merchant IDs for Apple Pay

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Capability changes require a profile regeneration</div>
    <p>
      When you add or remove a capability from a bundle ID in ASC, the existing provisioning profile for that bundle ID becomes stale. Regenerate the profile after any capability change.
    </p>
  </div>
</div>
