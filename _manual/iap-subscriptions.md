---
layout: manual
title: "In-App Purchases & Subscriptions"
description: "Create and manage in-app purchases and auto-renewable subscriptions in Mainline."
breadcrumb: true
permalink: /manual/iap-subscriptions/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>In-App Purchases &amp; Subscriptions</h1>
  <p>Create products, set pricing tiers, configure introductory offers, and manage subscription groups.</p>
</div>

<!-- SCREENSHOT: iap-list -->
<div class="screenshot-placeholder">
  <span class="ph-icon">💳</span>
  <span class="ph-label">Products list — subscriptions and one-time purchases</span>
  <span class="ph-hint"><!-- SCREENSHOT: iap-products-list --></span>
</div>

## Products section

The **Products** section is accessible from the App Detail view. It lists all your in-app purchases and auto-renewable subscriptions, grouped by type.

Tap any product to view its current configuration.

---

## Creating an in-app purchase

<ol class="steps">
  <li>Tap the <strong>+</strong> button in the Products section header and choose <strong>In-App Purchase</strong>.</li>
  <li>Choose the purchase type: <strong>Consumable</strong>, <strong>Non-Consumable</strong>, or <strong>Non-Renewing Subscription</strong>.</li>
  <li>Enter a <strong>Reference Name</strong> (internal name, visible only to you) and a <strong>Product ID</strong> (e.g. <code>com.example.yourapp.premium_unlock</code>).</li>
  <li>Select a <strong>pricing tier</strong>.</li>
  <li>Add a <strong>Display Name</strong> and <strong>Description</strong> for your primary locale.</li>
  <li>Tap <strong>Create</strong>. Mainline creates the product on App Store Connect.</li>
</ol>

---

## Creating a subscription

<ol class="steps">
  <li>Tap the <strong>+</strong> button and choose <strong>Auto-Renewable Subscription</strong>.</li>
  <li>Select a <strong>Subscription Group</strong>, or create a new group. Each subscription must belong to a group.</li>
  <li>Enter a <strong>Reference Name</strong>, <strong>Product ID</strong>, and <strong>Subscription Duration</strong> (weekly, monthly, 3 months, 6 months, annual).</li>
  <li>Choose a <strong>pricing tier</strong>. Mainline sets up pricing for your base territory automatically; you can add territory overrides later.</li>
  <li>Add a <strong>Display Name</strong> and optional <strong>Description</strong> for your primary locale.</li>
  <li>Tap <strong>Create</strong>.</li>
</ol>

---

## Editing a product

Tap a product to open its detail view. You can edit:

- **Display Name** and **Description** per locale
- **Pricing tier** (base territory and overrides)
- **Introductory offer** configuration (for subscriptions)

### Introductory offers

For subscriptions, tap **Introductory Offer** to configure a free trial or discounted introductory period. You can set:

- **Offer type**: Free trial, Pay as you go, or Pay up front
- **Duration** and **period count**
- **Price** (for discounted offers)

Only one introductory offer is active at a time. Changes to introductory offers take effect after ASC processes them and your app is live.

---

## Per-territory pricing

Tap **Territory Pricing** on any product to override the pricing tier for individual storefronts. This is useful for markets where standard tier pricing doesn't map well to local purchasing power.

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Setting up territory pricing for subscriptions</div>
    <p>
      For subscriptions, territory pricing requires that the subscription's availability be confirmed first. If Mainline shows an error when you try to set territory pricing, check that the subscription is available in the relevant territory via <a href="{{ '/manual/pricing-availability/' | relative_url }}">Pricing &amp; Availability</a>.
    </p>
  </div>
</div>

---

## Subscription group localisations

Subscription groups have their own display name and promotional content, separate from individual subscription names. Edit these by tapping a group and choosing **Edit Group Localisations**. Changes to group localisations cascade to all subscriptions in the group — Mainline gives you per-subscription opt-out before applying.

---

## Common pitfalls

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Product IDs are permanent</div>
    <p>Once a product ID is set in ASC, it cannot be changed. Choose your naming scheme carefully before creating products.</p>
  </div>
</div>

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">Subscriptions require review approval before pricing changes take effect</div>
    <p>
      Pricing changes scheduled for the future work through ASC's approval workflow. Changes to a subscription's base price take effect at the next renewal cycle after approval.
    </p>
  </div>
</div>
