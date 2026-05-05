---
layout: manual
title: "Cert Repo & Match Repo"
description: "How Mainline stores and accesses your code-signing certificates and provisioning profiles in an encrypted GitHub repo."
breadcrumb: true
permalink: /manual/cert-repo/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Cert Repo &amp; Match Repo</h1>
  <p>Your signing assets, encrypted at rest in a private GitHub repo — compatible with fastlane match.</p>
</div>

## What is a cert repo?

A cert repo is a private GitHub repository that stores your code-signing certificates (as encrypted P12 files) and provisioning profiles. Mainline reads from this repo to import certs to the device Keychain and write them to GitHub Actions secrets for CI builds.

Mainline supports two formats:

| Format | Description |
|---|---|
| **fastlane match** | Standard match repo layout with AES-256-CBC + EVP_BytesToKey encryption. Passphrase is your `MATCH_PASSWORD`. |
| **Mainline custom (BYO)** | Mainline's own layout, compatible with `openssl enc`. Supports AES-256-CBC + PBKDF2 or EVP_BytesToKey. |

---

## Auto-detection

When you connect a cert repo during onboarding or from Settings, Mainline auto-detects the format and encryption scheme. It probes for:

1. A `Matchfile` in the repo root (indicates fastlane match)
2. A `mainline-manifest.json` (Mainline custom format)
3. A legacy `manifest.json`
4. Trial decryption with each supported scheme using the passphrase you provide

You don't need to tell Mainline which format you're using — it figures it out.

---

## Setting up a new cert repo

If you don't have an existing match repo, you can create one from scratch:

<ol class="steps">
  <li>Go to <strong>Settings → Cert Repo → Create New Repo</strong>.</li>
  <li>Choose a GitHub repository to use (create a new private repo first if needed).</li>
  <li>Set a strong passphrase. This will be your encryption key for all certs and profiles stored in the repo.</li>
  <li>Mainline initialises the repo with the Mainline custom format and stores the passphrase in the Keychain.</li>
</ol>

---

## Migrating from an existing repo

If you have an older-format cert repo (such as one using the legacy Mainline manifest format), Mainline can migrate it to the current format non-destructively — the original repo and its contents are preserved until you're satisfied with the migration.

Go to **Settings → Cert Repo → Migrate Repo**.

---

## Seeding the cert repo

If you have certs in your device Keychain but not yet in the repo, go to **Settings → Cert Repo → Upload Keychain Certs &amp; Profiles to Repo**. This reads your installed certs and profiles and writes encrypted copies to the repo.

---

## Orphan detection

During onboarding (and available any time from the cert repo settings), Mainline compares the manifest entries in your cert repo against the live state in ASC. Any cert or profile recorded in the manifest that no longer exists in ASC is highlighted as an **orphan**, with a one-tap **Remove** option that deletes the file and updates the manifest.

---

## Encryption schemes

| Scheme | Compatible with |
|---|---|
| AES-256-CBC + EVP_BytesToKey | fastlane match, most existing match repos |
| AES-256-CBC + PBKDF2 | Modern openssl encryption, Mainline custom format |
| Plaintext | No encryption — private-repo access only |

> **Not supported:** GPG / SOPS / age / git-crypt. If your repo uses one of these, convert to a supported scheme first.

---

## Security model

- The cert repo passphrase is stored in the **iOS Keychain**, not in plain text or user defaults.
- Mainline only reads from and writes to your cert repo using the GitHub PAT you provide — it never handles your credentials through any AG Studio Apps server.
- Encryption and decryption happen entirely on-device. The passphrase never leaves your device.

See the [Privacy Policy]({{ '/mainline_docs/privacy/' | relative_url }}) for full details on how credentials are handled.
