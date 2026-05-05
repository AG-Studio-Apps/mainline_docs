---
layout: manual
title: "Settings"
description: "Auto-sync, cert repo management, AI provider configuration, and plan management in Mainline."
breadcrumb: true
permalink: /mainline_docs/manual/settings/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Settings</h1>
  <p>Manage your connections, auto-sync behaviour, cert repo, AI provider, and subscription plan.</p>
</div>

## Accessing Settings

Tap the **gear icon** in the top-right corner of the Dashboard (or the Onboarding screen) to open Settings.

---

## Connections

The Connections section shows all your configured credentials:

- **App Store Connect** — key status (connected / not connected), with an option to replace the key
- **GitHub** — PAT status, with an option to replace the token
- **Cert Repo** — which repo is configured and which format was detected, with options to change or reconfigure
- **AI Provider** — which providers are connected, active provider selection, and model selection

---

## Auto-sync

**Auto-sync on launch** fetches the latest cert and profile state from ASC and your cert repo each time you open Mainline.

This setting is **off by default**. Enabling it means Face ID (or your device passcode) is requested on every app launch because the sync reads credentials from the Keychain. Most users prefer to sync manually using the Dashboard's Sync button.

---

## Cert Repo management

Under **Settings → Cert Repo** you can:

| Action | Description |
|---|---|
| **Add / Change Repo** | Connect a different cert repo |
| **Create New Repo** | Initialise a new blank cert repo in an existing GitHub repo |
| **Migrate Repo** | Migrate from a legacy format to the current format |
| **Upload Keychain Certs &amp; Profiles** | Seed the repo with certs and profiles currently installed in the Keychain |
| **Use Existing Match Repo** | Point Mainline at an existing fastlane match repo |

---

## AI Provider

Under **Settings → AI Provider** you can:

- Set the **active provider** (Anthropic or OpenAI)
- Choose the **model** to use for each provider
- Update your **API key** for either provider

---

## Plan

Under **Settings → Plan** you can:

- View your current plan (Free or Pro)
- **Upgrade to Pro** via in-app purchase (monthly or annual)
- **Change your pinned app** (free tier only) — shows the cooldown remaining if within 90 days of your last pin
- **Restore Purchases** — if you've subscribed on another device

---

## Observability log

The **Activity Log** (accessible from Settings) shows a log of recent API calls Mainline has made — requests, responses, and any errors. This is primarily a diagnostic tool for troubleshooting. Log entries are stored locally and redacted of sensitive values before display.
