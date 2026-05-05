---
layout: page
title: "End User Licence Agreement"
description: "The End User Licence Agreement for Mainline, the iOS app for indie iOS developers."
---

<div class="page-header">
  <div class="page-header__eyebrow">Legal</div>
  <h1>End User Licence Agreement</h1>
  <p>Please read this agreement carefully before using Mainline.</p>
</div>

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">This is not legal advice</div>
    <p>
      This document has not been reviewed by a solicitor and is provided for informational purposes. Nothing in this agreement constitutes legal advice. If you need legal advice, please consult a qualified solicitor.
    </p>
  </div>
</div>

**Last updated:** <<YYYY-MM-DD>>

This End User Licence Agreement ("Agreement") is a legal agreement between you ("User", "you") and **AG Studio Apps** ("we", "us", "our") for the use of **Mainline** (the "App"). By downloading, installing, or using the App, you agree to be bound by this Agreement. If you do not agree, do not download, install, or use the App.

---

## 1. Licence Grant

Subject to your compliance with this Agreement, we grant you a limited, non-exclusive, non-transferable, revocable licence to:

1. Download and install the App on iOS devices that you own or control.
2. Use the App for your personal and commercial purposes as an app developer managing your own App Store Connect account(s).

This licence does not include the right to sublicence, sell, resell, transfer, assign, distribute, or otherwise commercially exploit the App to third parties. You may not copy, modify, adapt, translate, reverse engineer, decompile, disassemble, or create derivative works of the App or any part of it.

---

## 2. User Responsibilities

### 2.1 Your Credentials

The App requires you to provide credentials including, but not limited to:

- App Store Connect API keys (`.p8` private key files, Key ID, and Issuer ID)
- GitHub Personal Access Tokens
- AI provider API keys (Anthropic, OpenAI, or similar)
- Code-signing certificates and provisioning profiles
- Cert repo encryption passphrases

**You are solely responsible** for the security of your credentials, the permissions you assign to them, and any actions taken using them. By providing credentials to the App, you authorise Mainline to use those credentials to make API calls on your behalf to the relevant third-party services (Apple's App Store Connect API, GitHub's API, and your chosen AI provider).

### 2.2 Actions on Third-Party Services

The App interacts with third-party services — principally Apple's App Store Connect API, GitHub, and AI provider APIs — on your behalf using the credentials you supply. You acknowledge that:

- You are responsible for all actions taken through those services via Mainline.
- You must comply with the terms of service of each third-party service you use through the App.
- We are not responsible for any consequences of actions you take through the App on those services.

### 2.3 Content You Publish

You are responsible for all content you choose to publish to App Store Connect through the App, including metadata, descriptions, screenshots, and other listing material, whether drafted by you directly or with AI assistance (see section 6).

### 2.4 Acceptable Use

You must not use the App to:

- Violate any applicable law or regulation
- Infringe the intellectual property rights of any third party
- Submit false, misleading, or fraudulent information to App Store Connect or any other service
- Circumvent or attempt to circumvent the terms of service of Apple, GitHub, or any other third-party service

---

## 3. Subscription and Payment

### 3.1 Free Tier

The App is available free of charge with limited functionality (one pinned app, with a 90-day cooldown for changing the pinned app).

### 3.2 Mainline Pro

Additional functionality is available through **Mainline Pro**, an auto-renewable subscription available for purchase within the App. Subscription pricing is displayed within the App at the time of purchase.

### 3.3 Billing

All subscription transactions are processed by Apple via the App Store. By subscribing, you agree to Apple's payment terms. We do not collect, store, or process payment information directly.

### 3.4 Cancellation and Refunds

You may cancel your subscription at any time through your Apple ID settings. Cancellation takes effect at the end of the current billing period. Refunds are subject to Apple's refund policy. We have no ability to issue refunds directly.

---

## 4. Intellectual Property

### 4.1 Our IP

The App, including its name, branding, design, software, and all related materials, is the intellectual property of AG Studio Apps. All rights not expressly granted under this Agreement are reserved.

### 4.2 Feedback

If you provide feedback, suggestions, or ideas about the App, you grant us a perpetual, irrevocable, royalty-free licence to use, reproduce, modify, and incorporate that feedback into the App or other products without obligation to you.

### 4.3 Third-Party Content

The App integrates with third-party services and APIs. All trademarks, service marks, and trade names of those third parties (Apple, GitHub, Anthropic, OpenAI, etc.) are the property of their respective owners.

---

## 5. Privacy

Your use of the App is also governed by our [Privacy Policy]({{ '/privacy/' | relative_url }}), which is incorporated into this Agreement by reference. Please read it carefully.

---

## 6. AI Features

The App includes optional AI-assisted features that integrate large language models provided by Anthropic (Claude) and OpenAI, using API keys you supply.

**Important:**

- All AI-generated content is presented to you for review before any content is submitted to App Store Connect. The App does not automatically write AI-generated content to ASC without your explicit approval.
- You are solely responsible for reviewing AI-generated content and for any content you choose to publish based on AI suggestions.
- By using AI features, your content (such as app descriptions, metadata, and review replies) is sent to the AI provider you have selected using your own API key. This traffic goes directly from your device to the provider — we do not see or process this content. The provider's privacy policy applies to their handling of this data (see links in the [Privacy Policy]({{ '/privacy/' | relative_url }})).
- AI models may produce inaccurate, incomplete, or inappropriate outputs. Always review AI suggestions before applying them.

---

## 7. Disclaimer of Warranties

**To the maximum extent permitted by applicable law**, the App is provided **"AS IS"** and **"AS AVAILABLE"**, without warranty of any kind, either express or implied, including but not limited to:

- Warranties of merchantability or fitness for a particular purpose
- Warranties that the App will be uninterrupted, error-free, or secure
- Warranties regarding the accuracy or reliability of any API data retrieved through the App

**Nothing in this section excludes any statutory rights you may have as a consumer** under the laws of England and Wales or the Consumer Rights Act 2015, to the extent such rights cannot be excluded by contract.

---

## 8. Limitation of Liability

**To the maximum extent permitted by applicable law**, in no event shall AG Studio Apps be liable for:

- Indirect, incidental, special, exemplary, or consequential damages
- Loss of profits, revenue, data, business, or goodwill
- Any damages resulting from your use of third-party services accessed through the App (including App Store Connect, GitHub, or AI providers)
- Any damages resulting from AI-generated content that you choose to publish

Our total aggregate liability to you for any claims arising under this Agreement shall not exceed the amount paid by you for the App in the 12 months immediately preceding the claim.

**Nothing in this section limits our liability** for death or personal injury caused by our negligence, fraud or fraudulent misrepresentation, or any other liability that cannot be limited by law under English law.

---

## 9. Indemnification

You agree to indemnify and hold harmless AG Studio Apps and its directors, officers, employees, and agents from any claims, losses, damages, liabilities, and expenses (including reasonable legal fees) arising from:

- Your use of the App
- Your breach of this Agreement
- Any content you publish to App Store Connect through the App
- Your violation of any third-party rights or terms of service

---

## 10. Third-Party Services

The App integrates with third-party services. Your use of those services is governed by their respective terms of service and privacy policies:

- **Apple App Store Connect API** — developer.apple.com
- **GitHub API** — github.com/site/terms
- **Anthropic** — anthropic.com/legal/privacy
- **OpenAI** — openai.com/policies/privacy-policy

We are not responsible for the availability, accuracy, or content of third-party services.

---

## 11. Updates and Changes to the App

We may update the App from time to time. Updates may change or remove features. We may also discontinue the App; in such a case, we will provide reasonable notice where possible.

---

## 12. Changes to This Agreement

We may update this Agreement at any time. If we make material changes, we will notify you through the App or by posting an updated version here. Your continued use of the App after changes take effect constitutes acceptance of the revised Agreement.

---

## 13. Termination

This Agreement is effective until terminated. Your rights under this Agreement terminate automatically without notice if you breach any term. Upon termination, you must stop using the App and delete all copies. Sections 4, 6, 7, 8, 9, and 14 survive termination.

---

## 14. Governing Law and Disputes

This Agreement is governed by the laws of **England and Wales**. Any disputes arising from this Agreement shall be subject to the exclusive jurisdiction of the courts of England and Wales.

If you are a consumer resident in a European Union member state, you may also have rights under the laws of your country of residence.

---

## 15. Contact

For questions about this Agreement, contact us at: **<<contact-email>>**
