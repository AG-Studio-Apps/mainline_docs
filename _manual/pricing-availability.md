---
layout: manual
title: "Pricing & Availability"
description: "Set your app's base price, manage territory overrides, and control which storefronts it's available in."
breadcrumb: true
permalink: /mainline_docs/manual/pricing-availability/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Pricing &amp; Availability</h1>
  <p>Set your app's base price, manage territory overrides, and control which storefronts it's available in.</p>
</div>

## App pricing

Your app's price is set from the **Pricing &amp; Availability** section inside the App Detail view. Tap **Change Price** to select a price tier.

ASC uses a tier system (Free, Tier 1, Tier 2, etc.) — you pick a tier and Apple maps it to local currency prices across all storefronts.

### Territory price overrides

If you want different pricing in specific countries, tap **Territory Overrides** to set per-storefront prices. Select a territory, choose an override tier, and save. Overrides are applied on top of the base tier.

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Per-territory pricing for in-app purchases</div>
    <p>
      Territory overrides for in-app purchases and subscriptions are managed separately from the app's base price. See <a href="{{ '/mainline_docs/manual/iap-subscriptions/' | relative_url }}">In-App Purchases &amp; Subscriptions</a>.
    </p>
  </div>
</div>

---

## Availability (territories)

Tap **Manage Availability** to control which countries and regions your app is available in. By default, new apps are available in all territories.

You can:
- Remove specific territories to restrict distribution
- Re-add territories to expand distribution

Changes to availability take effect immediately for future downloads; they don't affect users who have already purchased or downloaded your app.

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Cannot set per-territory pricing from the app yet</div>
    <p>
      Deep-link per-territory pricing on the app price schedule (as opposed to IAP territory overrides) currently opens App Store Connect in Safari. This will be addressed in a future update.
    </p>
  </div>
</div>
