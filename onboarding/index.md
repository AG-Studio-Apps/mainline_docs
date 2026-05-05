---
layout: page
title: "Getting Started with Mainline"
description: "A step-by-step guide to setting up Mainline after you install it — connecting your App Store Connect key, GitHub, cert repo, and AI provider."
---

<div class="page-header">
  <div class="page-header__eyebrow">Onboarding</div>
  <h1>Getting Started</h1>
  <p>You've just installed Mainline. Here's how to go from zero to managing your apps in a few minutes.</p>
</div>

<!-- SCREENSHOT: onboarding-welcome -->
<div class="screenshot-placeholder">
  <span class="ph-icon">📱</span>
  <span class="ph-label">Welcome screen — setup wizard</span>
  <span class="ph-hint"><!-- SCREENSHOT: onboarding-welcome-step --></span>
</div>

Mainline uses a guided setup wizard that walks you through each connection in order. You can also tap any item in the **Connections** list to handle them in your own order, or skip optional steps and come back to them later from **Settings**.

---

## What you'll need

| Requirement | Where to get it | Required? |
|---|---|---|
| App Store Connect API key (`.p8` file) | App Store Connect → Users and Access → Integrations | **Yes** |
| ASC Key ID | Same page, shown next to the key name | **Yes** |
| ASC Issuer ID | Same page, shown at the top of the Integrations tab | **Yes** |
| GitHub Personal Access Token | GitHub → Settings → Developer settings → Personal access tokens | Optional (for CI features) |
| Cert repo + passphrase | Your existing fastlane match repo, or a new one you create | Optional |
| Anthropic or OpenAI API key | anthropic.com/account or platform.openai.com | Optional (for AI features) |

---

## Step 1 — Connect App Store Connect

This is the only required step. Everything else is optional.

<ol class="steps">
  <li>
    <strong>Open App Store Connect in a browser.</strong> Go to <em>Users and Access → Integrations → App Store Connect API</em>.
  </li>
  <li>
    <strong>Create a new API key</strong> (or use one you already have). The key needs at least <em>App Manager</em> access. Download the <code>.p8</code> file — Apple only lets you download it once, so keep it safe.
  </li>
  <li>
    <strong>Note the Key ID and Issuer ID</strong> shown on the same page.
  </li>
  <li>
    <strong>In Mainline</strong>, tap <em>App Store Connect</em> in the setup wizard. Choose how to provide the key:
    <ul>
      <li><strong>Upload from files</strong> — import the <code>.p8</code> directly from Files or iCloud Drive, then type in the Key ID and Issuer ID.</li>
      <li><strong>Import from cert repo</strong> — if your <code>.p8</code> is already stored in a private GitHub repo, Mainline can read and extract it automatically. This path requires a GitHub PAT first (see Step 2).</li>
    </ul>
  </li>
  <li>
    Tap <strong>Continue</strong>. Mainline validates the key against App Store Connect and stores it securely in the iOS Keychain.
  </li>
</ol>

<details>
<summary>What is an App Store Connect API key?</summary>
<div class="details-body">
<p>
App Store Connect API keys let third-party tools (like Mainline) act on your behalf through Apple's official API. They're more secure than username/password because they carry only the permissions you assign and can be revoked individually. The <code>.p8</code> file is the private key; it's paired with a Key ID and Issuer ID that Mainline uses to sign API requests.
</p>
<p>
If you use fastlane or other CI tools, you likely already have one. You can reuse the same key — Mainline only reads it to make API calls, it never modifies or shares the file itself.
</p>
</div>
</details>

<details>
<summary>Which permission level do I need?</summary>
<div class="details-body">
<p>
<strong>App Manager</strong> is sufficient for most Mainline features: editing metadata, managing submissions, reading builds and reviews, and working with subscriptions.
</p>
<p>
<strong>Admin</strong> is required for a small number of operations, such as creating new bundle IDs, managing certificates, and inviting team members. If you're the account holder, you'll naturally have this.
</p>
<p>
If you're not the account holder, have the admin create the key with the access level appropriate for your role.
</p>
</div>
</details>

<!-- SCREENSHOT: asc-credentials-step -->
<div class="screenshot-placeholder">
  <span class="ph-icon">🔑</span>
  <span class="ph-label">ASC credentials entry screen</span>
  <span class="ph-hint"><!-- SCREENSHOT: onboarding-asc-credentials --></span>
</div>

---

## Step 2 — Connect GitHub (optional)

Connecting GitHub unlocks CI features: triggering workflows, monitoring run logs in real time, and writing the signing secrets your pipelines need.

<ol class="steps">
  <li>
    Go to <strong>GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens</strong> (or classic tokens).
  </li>
  <li>
    Create a token with the <strong><code>repo</code></strong> and <strong><code>workflow</code></strong> scopes. Fine-grained tokens: grant read/write access to <em>Actions</em> and <em>Secrets</em> on the repositories you want to manage.
  </li>
  <li>
    In Mainline, tap <strong>GitHub</strong> in the setup wizard, paste your token, and tap <strong>Validate &amp; Save</strong>. Mainline checks the token against the GitHub API and stores it in the Keychain.
  </li>
</ol>

<details>
<summary>What scopes does Mainline need?</summary>
<div class="details-body">
<p>
Mainline needs <strong><code>repo</code></strong> to read your repositories and the cert repo, and <strong><code>workflow</code></strong> to trigger and read GitHub Actions runs. If you use fine-grained tokens, grant equivalent permissions on the specific repositories you want Mainline to manage.
</p>
<p>
Mainline never modifies your source code. The only writes it makes to GitHub repos are: (a) updating secrets used for signing, and (b) writing to the cert repo when you sync certificates or profiles.
</p>
</div>
</details>

---

## Step 3 — Connect a cert repo (optional)

A cert repo is a private GitHub repository that stores your code-signing certificates (P12 files) and provisioning profiles in encrypted form. Mainline supports two formats:

- **fastlane match repos** — if you already use fastlane match, point Mainline at that repo and give it your `MATCH_PASSWORD`.
- **Custom (BYO) repos** — Mainline's own format, compatible with `openssl enc`-encrypted files.

<ol class="steps">
  <li>
    In Mainline, tap <strong>Certificates Repo</strong> in the setup wizard. (You need a GitHub PAT connected first.)
  </li>
  <li>
    <strong>Pick a repo</strong> from the list of your GitHub repositories.
  </li>
  <li>
    Enter the <strong>repo encryption passphrase</strong>. This is <em>not</em> your GitHub password — it's the passphrase used to encrypt files inside the repo (your <code>MATCH_PASSWORD</code> for fastlane match, or the passphrase you used with <code>openssl enc</code>). Leave it empty for plaintext repos.
  </li>
  <li>
    Tap <strong>Continue</strong>. Mainline auto-detects the repo format and encryption scheme, then stores the configuration.
  </li>
</ol>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">No cert repo yet?</div>
    <p>
      You can skip this step and set it up later from <strong>Settings → Cert Repo</strong>. Mainline can manage your app metadata, builds, and submissions without a cert repo — you'll just need one when you want Mainline to inject signing credentials into your CI pipeline.
    </p>
  </div>
</div>

**Supported encryption schemes:**

| Scheme | Description |
|---|---|
| Plaintext | Raw files, private-repo access only |
| AES-256-CBC + EVP_BytesToKey | fastlane match style |
| AES-256-CBC + PBKDF2 | Modern openssl / Mainline custom format |

> **Not supported:** GPG, SOPS, age, git-crypt. Convert to one of the above first.

---

## Step 4 — Sync certificates to Keychain (optional)

After configuring the cert repo, Mainline offers to pull your team's distribution certificates and provisioning profiles from ASC and your repo into the device Keychain. This means your first CI build won't need a re-fetch.

You can do this now or skip it — the **Sync** button on the Dashboard does the same thing at any time.

---

## Step 5 — Connect an AI provider (optional)

Connecting an AI provider unlocks AI-assisted features: translation, metadata drafting, and review-reply suggestions. You can use Anthropic (Claude) or OpenAI (ChatGPT), or both.

<ol class="steps">
  <li>Get an API key from <a href="https://console.anthropic.com" target="_blank" rel="noopener">console.anthropic.com</a> or <a href="https://platform.openai.com" target="_blank" rel="noopener">platform.openai.com</a>.</li>
  <li>In Mainline, tap <strong>AI Provider</strong> in the setup wizard and paste your key(s).</li>
  <li>Tap <strong>Save</strong>. You can change provider and model any time in <strong>Settings → AI Provider</strong>.</li>
</ol>

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">AI is always human-in-the-loop</div>
    <p>
      Every piece of AI-generated content — translations, drafted descriptions, reply suggestions — is shown to you for review before anything is sent to App Store Connect. Mainline never writes AI content directly to ASC.
    </p>
  </div>
</div>

---

## You're set up — what's next?

Once App Store Connect is connected, tap **Continue to Dashboard**. You'll see all your apps pulled from ASC.

From here, explore the features you need most:

- **[App Listings]({{ '/mainline_docs/manual/listings/' | relative_url }})** — edit metadata per locale
- **[TestFlight Builds]({{ '/mainline_docs/manual/testflight/' | relative_url }})** — view and manage builds
- **[Submission]({{ '/mainline_docs/manual/submission/' | relative_url }})** — submit for review
- **[In-App Purchases]({{ '/mainline_docs/manual/iap-subscriptions/' | relative_url }})** — manage products and subscriptions

---

## Free vs Pro {#free-vs-pro}

Mainline is free to use with one pinned app. The free tier includes all features — there are no feature-level restrictions, only an app-count limit.

### Free tier

- **One app pinned** — you choose which app to manage. All features available for that app.
- **Read-only for other apps** — you can browse your other apps but cannot make changes.
- **Re-pin with a cooldown** — you can change your pinned app, but there's a **90-day waiting period** between re-pins. This is to prevent the free tier from being equivalent to a Pro subscription.

### Mainline Pro

- **Unlimited apps** — full read and write access for every app in your ASC account.
- Billed monthly or annually via in-app purchase.

### Pinning an app

When you first open the Dashboard, Mainline automatically pins your first app if you only have one. If you have multiple apps, you'll be prompted to choose one to pin.

### The 90-day re-pin cooldown

If you want to switch your pinned app, you can do so from **Settings → Plan**. The cooldown timer starts from the last time you pinned an app. If you're within the cooldown window, the re-pin option shows how long is left.

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Just one app?</div>
    <p>
      If your ASC account only has one app, you never hit the free-tier limit in practice — read and write access is always on for your sole app.
    </p>
  </div>
</div>
