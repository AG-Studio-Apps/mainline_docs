---
layout: manual
title: "Dashboard"
description: "An overview of the Mainline dashboard — your apps, signing health, and quick-action cards."
breadcrumb: true
permalink: /mainline_docs/manual/dashboard/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Dashboard</h1>
  <p>The central view of Mainline — your apps, signing health, and everything one tap away.</p>
</div>

<!-- SCREENSHOT: dashboard-main -->
<div class="screenshot-placeholder">
  <span class="ph-icon">🏠</span>
  <span class="ph-label">Dashboard — apps list view</span>
  <span class="ph-hint"><!-- SCREENSHOT: dashboard-main-view --></span>
</div>

## What the Dashboard shows

When you open Mainline, the **Dashboard** appears. It pulls your apps from App Store Connect and organises them into cards. Each card shows:

- App name and icon
- Current live version and App Store status
- Signing health indicator (whether certificates and profiles are valid)
- Quick links to builds, CI runs, and the app detail view

### Signing health

The signing indicator reflects the state of your certificates and provisioning profiles. If a cert is expiring soon or a profile has been regenerated in ASC since your last sync, the indicator turns orange or red.

Tap the indicator to open the **Certificates & Profiles** view for that app, where you can renew or re-sync.

---

## App detail

Tapping an app card opens the **App Detail** view, which is the main workspace for that app. It's organised into sections:

| Section | What's here |
|---|---|
| **Listing** | Metadata fields — name, subtitle, description, keywords, What's New |
| **Builds** | TestFlight builds attached to the current version |
| **Submission** | Review submission status, phased release controls |
| **Products** | In-app purchases and subscriptions |
| **Reviews** | Recent customer reviews with reply capability |
| **CI Runs** | Recent GitHub Actions runs for this app's repo |
| **Certificates** | Certs and profiles for this bundle ID |

---

## New App Wizard

Tap the **+** button in the Dashboard toolbar to launch the **New App Wizard**. This guides you through:

1. Creating a bundle ID in ASC (with capability selection)
2. Creating the app record on App Store Connect
3. Setting up the initial signing configuration

The wizard hands off to ASC for the final "Create App" step that requires a human to confirm in the browser.

---

## Architecture Planning Wizard

For new apps, Mainline includes an **Architecture Planning** tool that uses AI to help you think through your app's technical design — data model, sync strategy, monetisation approach. This is an AI-assisted planning aid, not a code generator.

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Architecture plans live locally</div>
    <p>Plans are stored on your device. They're a thinking tool — nothing is sent to ASC or GitHub unless you explicitly choose to act on the output.</p>
  </div>
</div>

---

## Onboarding checklist

Until all connections are set up, the Dashboard shows an **Onboarding Checklist** card that tracks your progress:

- App Store Connect: connected or not
- GitHub: connected or not
- Cert repo: configured or skipped
- AI provider: connected or skipped
- App pinned (free tier): done or pending

Each row is tappable and takes you directly to the relevant setup step. Once everything is either connected or deliberately skipped, the checklist disappears.

---

## Sync

The **Sync** button (top-right toolbar menu) fetches the latest cert and profile state from ASC and your cert repo, then updates the Keychain. Run this after renewing a certificate or regenerating a profile to pull the new assets to your device.

Auto-sync on app launch is available in Settings but is off by default, as it triggers Face ID on every open.

---

## Common pitfalls

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Read-only banner on non-pinned apps</div>
    <p>
      On the free tier, apps that aren't your pinned app show a <strong>read-only banner</strong>. You can browse all their details but write actions (editing metadata, triggering builds, submitting for review) are disabled. Pin the app or upgrade to Pro to enable writes.
    </p>
  </div>
</div>
