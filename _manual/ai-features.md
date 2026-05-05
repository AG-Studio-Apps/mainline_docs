---
layout: manual
title: "AI Features"
description: "AI-assisted translation, metadata drafting, review replies, and architecture planning — all human-in-the-loop."
breadcrumb: true
permalink: /mainline_docs/manual/ai-features/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>AI Features</h1>
  <p>Translation, metadata drafting, review-reply suggestions, and architecture planning — with a human review gate before anything reaches App Store Connect.</p>
</div>

## The core principle: human-in-the-loop

Every piece of AI-generated content in Mainline passes through a **review-and-accept step** before it is sent to App Store Connect. Mainline never writes AI-generated content directly to ASC. You always see what the AI produced, can edit it freely, and decide whether to apply it.

This applies to:
- Translated listing fields
- Drafted descriptions and promotional text
- Review reply suggestions
- Architecture plans (not sent to ASC at all — stored locally)

---

## Supported providers

| Provider | Models |
|---|---|
| **Anthropic** | Claude (model selection in Settings) |
| **OpenAI** | GPT-4 and later (model selection in Settings) |

You connect your own API key — Mainline sends requests directly from your device to the provider. AG Studio Apps never sees your content or your API keys. See the [Privacy Policy]({{ '/mainline_docs/privacy/' | relative_url }}) for details.

---

## AI Translation

AI translation is available on every listing text field. After saving a field in one locale, tap **Translate to other locales**.

### How it works

<ol class="steps">
  <li>You see a list of your app's other active locales.</li>
  <li>Select the locales you want to translate into.</li>
  <li>Optionally toggle <strong>Overwrite populated fields</strong> — if off, Mainline skips locales that already have content for this field.</li>
  <li>Tap <strong>Translate</strong>. Mainline runs translations concurrently, with a concurrency limit to avoid hitting rate limits.</li>
  <li>Each locale shows its result: the translated text, a success indicator, or an error.</li>
  <li>Tap <strong>Apply</strong> on individual locales, or <strong>Apply All</strong>.</li>
</ol>

### Character limits

Mainline enforces ASC's character limits client-side before each PATCH. If a translation exceeds the limit for a field, you're shown the translated text and asked to shorten it — Mainline won't silently truncate.

---

## AI Metadata Drafting

On the description, promotional text, and What's New fields, tap **Draft with AI** to generate a draft from scratch.

Mainline sends your app name, existing metadata context, and an optional brief you provide as a prompt. The draft appears in the editor for you to revise before saving.

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">The draft is a starting point</div>
    <p>
      AI-drafted copy rarely goes directly to the App Store without editing. Use it to break writer's block or get a structure in place, then revise for your app's voice.
    </p>
  </div>
</div>

---

## AI Review Reply Suggestions

When replying to a customer review, tap **Suggest Reply**. Mainline sends the review text to your AI provider and generates a suggested response. The suggestion appears in the reply editor — you edit it, accept it, or start fresh.

---

## Architecture Planning Wizard

For new apps, the **Architecture Planning Wizard** is an AI-assisted planning tool. It asks you questions about your app's purpose, target users, key features, and technical requirements, then generates a structured technical plan covering:

- Data model recommendations
- Sync and persistence strategy
- Monetisation approach
- Key technical considerations

Plans are stored locally on your device. Nothing is sent to ASC or GitHub. The wizard is available from the Dashboard toolbar menu.

---

## Configuring your AI provider

Go to **Settings → AI Provider** to:

- Switch between Anthropic and OpenAI as the active provider
- Select the specific model to use
- Update your API key

You can connect both providers and switch between them at any time.

---

## AI usage costs

Mainline uses your own API keys. All usage charges go directly from you to your chosen AI provider — AG Studio Apps does not mark up or proxy AI usage. Check your provider's current pricing before running large batch operations like translating many locales at once.
