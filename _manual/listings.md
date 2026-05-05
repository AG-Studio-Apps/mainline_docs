---
layout: manual
title: "App Listings"
description: "Edit your app's name, subtitle, description, keywords, promotional text, and What's New notes across every locale."
breadcrumb: true
permalink: /mainline_docs/manual/listings/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>App Listings</h1>
  <p>Edit every text field on your App Store listing — per-locale — and translate to other languages in one step.</p>
</div>

<!-- SCREENSHOT: listing-editor -->
<div class="screenshot-placeholder">
  <span class="ph-icon">📝</span>
  <span class="ph-label">Listing editor — description field</span>
  <span class="ph-hint"><!-- SCREENSHOT: listing-editor-description --></span>
</div>

## What you can edit

All editable listing fields are available in Mainline:

| Field | Limit | Notes |
|---|---|---|
| **Name** | 30 characters | Shared across all locales |
| **Subtitle** | 30 characters | Per-locale |
| **Description** | 4,000 characters | Per-locale |
| **Keywords** | 100 characters | Per-locale, comma-separated |
| **Promotional text** | 170 characters | Per-locale; updateable without a new submission |
| **What's New** | 4,000 characters | Per-locale; shown in the update notification |

Changes are written to the **current (editable) version** of your app. If there's no editable version, Mainline prompts you to create one first.

---

## Editing a field

<ol class="steps">
  <li>Open the app from the Dashboard and tap the <strong>Listing</strong> section.</li>
  <li>Select a <strong>locale</strong> from the locale picker. The primary locale is shown first.</li>
  <li>Tap a field to open the editor. The editor shows the character count and limit as you type.</li>
  <li>Tap <strong>Save</strong>. The change is sent to App Store Connect immediately. If ASC returns a conflict (e.g. someone else edited the same field), Mainline shows the conflict inline — you choose to overwrite or discard.</li>
</ol>

---

## Managing locales

Tap **Add Locale** to add a new language to your listing. Mainline shows all locales supported by ASC. Tap a locale to switch to it; the editor re-loads the field values for that locale.

---

## Translating to other locales

After saving a field in one locale, Mainline offers a **Translate to other locales** action. This:

1. Takes the text you just saved (in the source locale) as input.
2. Shows you a list of your app's other active locales to translate into.
3. Runs AI translation for each selected locale (using your configured AI provider).
4. Shows you each translated result for review before sending it to ASC.
5. PATCHes only the locales you approve.

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Human review is mandatory</div>
    <p>
      Every translation is shown to you before it goes to ASC. You can edit the AI-generated text or discard it entirely. Mainline enforces ASC's character limits client-side — you'll be warned before a truncation is needed.
    </p>
  </div>
</div>

---

## AI-assisted drafting

Tap the **Draft with AI** button (shown on description and What's New fields) to generate a draft from a brief prompt or your existing app context. The drafted text appears in the editor for you to review and edit before saving.

See [AI Features]({{ '/mainline_docs/manual/ai-features/' | relative_url }}) for more detail on how AI drafting works.

---

## Copying from a previous version

When you start a new version for an existing app, Mainline offers to copy listing content from the live version. This is useful when your update is minor and you only need to change What's New.

---

## App Store Search Preview

The **Search Preview** button (shown in the Listing section header) renders a mock App Store search result using your current name, subtitle, and first screenshot. It's a sanity check — not a pixel-perfect simulation — to catch truncation and phrasing issues before submission.

---

## Common pitfalls

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Some characters are banned by ASC</div>
    <p>
      App Store Connect rejects certain typographic characters in description fields, including em dashes and en dashes. Mainline's editor warns you if you paste text containing banned characters before you attempt to save.
    </p>
  </div>
</div>

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Promotional text updates without a new submission</div>
    <p>
      Promotional text is the only listing field you can update on a live version without submitting a new build for review. All other fields require an editable (pre-review) version.
    </p>
  </div>
</div>
