---
layout: page
title: "Privacy Policy"
description: "How Mainline handles your data — spoiler: we don't collect any."
---

<div class="page-header">
  <div class="page-header__eyebrow">Legal</div>
  <h1>Privacy Policy</h1>
  <p>What data Mainline collects, where it goes, and what we do with it.</p>
</div>

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">This is not legal advice</div>
    <p>
      This document has not been reviewed by a solicitor and is provided for informational purposes. If you need legal advice about data protection, please consult a qualified solicitor.
    </p>
  </div>
</div>

**Effective date:** 2026-05-05

This Privacy Policy describes how **AG Studio Apps** ("we", "us", "our") handles information in connection with your use of **Mainline** (the "App").

**Short version:** Mainline operates without a backend server. We don't collect your personal data, don't run analytics, and don't have access to your credentials or content. The one narrow exception is an anonymous iCloud record described in Section 3.

---

## 1. No backend, no data collection

Mainline does **not** operate any backend server or cloud infrastructure maintained by AG Studio Apps.

All API calls the App makes go directly from your device to:

- **Apple's App Store Connect API** (`api.appstoreconnect.apple.com`)
- **GitHub's API** (`api.github.com`)
- **Your chosen AI provider** (Anthropic or OpenAI), when you invoke AI features

AG Studio Apps never receives, routes, or processes these API calls. We have no visibility into your App Store Connect data, your GitHub repositories, or any content you work with in the App.

---

## 2. Credentials stored on-device only

The following sensitive credentials are stored exclusively in your device's **iOS Keychain** and never transmitted to AG Studio Apps:

- App Store Connect API private key (`.p8`)
- App Store Connect Key ID and Issuer ID
- GitHub Personal Access Token
- AI provider API keys (Anthropic and/or OpenAI)
- Code-signing certificate private keys (P12 files)
- Provisioning profile data
- Cert repo encryption passphrase

The iOS Keychain is a secure, encrypted store managed by the operating system. Access to Keychain items requires biometric authentication (Face ID or Touch ID) or your device passcode. These credentials are never synced to iCloud, never backed up in plain text, and never sent anywhere outside your device by Mainline.

---

## 3. iCloud: one record per ASC team

Mainline uses Apple's iCloud (CloudKit) for a single, narrow purpose: **enforcing the free tier's one-app-pinned constraint across device reinstalls and across the devices of the same ASC team**.

When you pin an app on the free tier, Mainline writes one record to Mainline's CloudKit container, accessed under your iCloud authentication. The record's identifier is a SHA-256 hash of your ASC Issuer ID — your raw Issuer ID is never stored in CloudKit. The record contains:

- The **bundle ID** of your pinned app
- A **timestamp** of when you originally pinned
- A **timestamp** of your most recent re-pin (drives the 90-day cooldown)

The record does **not** contain your name, email address, Apple ID, ASC Issuer ID, or any other personal identifier — only the bundle ID of the app you've chosen to manage on free, plus the two timestamps.

A copy of the same record is also stored in your iOS Keychain with iCloud Keychain sync enabled, as a fallback when CloudKit is unavailable. iCloud Keychain is end-to-end encrypted by Apple between the devices signed in with your Apple ID.

If you delete the App, the record remains in CloudKit until you manually clear it. You can do so via **Settings → Apple ID → iCloud → Manage Account Storage → Mainline** on your device, or by upgrading to Pro (which retires the free-tier record).

---

## 4. In-app purchases

Mainline Pro is an auto-renewable subscription purchased through the App Store. All payment processing is handled exclusively by Apple. Mainline receives only a signed transaction receipt from StoreKit — we never see your payment card details, billing address, or Apple ID.

---

## 5. AI features: your content, your provider

When you use AI features in Mainline (translation, metadata drafting, review reply suggestions), Mainline sends content from your App Store Connect listings — such as description text, promotional copy, or review text — to your chosen AI provider using the API key you supplied.

**This traffic goes directly from your device to the AI provider.** AG Studio Apps does not see, store, or process this content.

By using AI features, you are subject to the privacy policy of your chosen provider:

- **Anthropic:** [anthropic.com/legal/privacy](https://www.anthropic.com/legal/privacy)
- **OpenAI:** [openai.com/policies/privacy-policy](https://openai.com/policies/privacy-policy)

We recommend reviewing your provider's data retention and training policies before submitting sensitive content.

---

## 6. No analytics, no telemetry, no advertising

Mainline contains:

- **No analytics SDK** (no Firebase, Mixpanel, Amplitude, or equivalent)
- **No crash reporting SDK** that transmits to a third-party server
- **No advertising SDK**
- **No third-party tracking or attribution SDK**
- **No cookies** (it is a native iOS app, not a web app)

The App's **Activity Log** (accessible from Settings) is a local diagnostic log stored exclusively on your device. It is never transmitted to AG Studio Apps.

---

## 7. Children's privacy

Mainline is a developer tool intended for use by app developers. It is not directed at or intended for children under the age of 13. We do not knowingly collect personal information from children. If you believe a child under 13 has provided personal information through the App, please contact us.

---

## 8. Data retention

Because we do not collect personal data, there is nothing for us to retain or delete. Credentials and app configuration are stored in the iOS Keychain and device storage; you can delete them at any time by removing the App.

The single iCloud record described in Section 3 is stored in your own iCloud account. You can delete it via your device's iCloud settings.

---

## 9. Your rights

Depending on your location, you may have rights under applicable data protection laws (such as the UK GDPR or EU GDPR), including:

- The right to access personal data we hold about you
- The right to rectification or erasure
- The right to data portability
- The right to object to processing

Because we do not collect or process personal data beyond the iCloud record described in Section 3 (which is in your own iCloud account), most of these rights are satisfied by the fact that your data stays with you. If you have a query or request relating to your data, contact us at **james@agnticstudio.com**.

---

## 10. Security

We take reasonable steps to protect the App from known security vulnerabilities. Credentials are stored using OS-level security primitives (iOS Keychain). We do not store credentials on our servers because we do not have servers that handle your credentials.

---

## 11. Changes to this policy

We may update this Privacy Policy from time to time. Material changes will be communicated through the App or by posting an updated version here. The effective date at the top of this page will be updated accordingly.

---

## 12. Contact

If you have questions about this Privacy Policy, contact us at: **james@agnticstudio.com**
