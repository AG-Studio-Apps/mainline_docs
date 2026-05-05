---
layout: manual
title: "Screenshots & Previews"
description: "Manage App Store screenshots and preview videos using Mainline's project-based renderer."
breadcrumb: true
permalink: /manual/screenshots/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Screenshots &amp; Previews</h1>
  <p>Organise, render, and upload App Store screenshots and preview videos — per device, per locale.</p>
</div>

<!-- SCREENSHOT: screenshots-list -->
<div class="screenshot-placeholder">
  <span class="ph-icon">🖼️</span>
  <span class="ph-label">Screenshots project list</span>
  <span class="ph-hint"><!-- SCREENSHOT: screenshots-project-list --></span>
</div>

## Screenshots tab

Mainline has a dedicated **Screenshots** tab, separate from the App Detail view. It uses a **project-based model** — you organise your screenshot assets into projects, then upload to one or more app versions from a project.

---

## Projects

A **project** is a collection of screenshot images grouped by device type and locale. You can have multiple projects (e.g. one per app, or one per major version) and reuse them across localizations.

### Creating a project

<ol class="steps">
  <li>Tap <strong>+</strong> in the Screenshots tab to create a new project.</li>
  <li>Give the project a name.</li>
  <li>Add images for each device class and locale you need. Drag images into device slots or use the document picker.</li>
</ol>

### Supported device classes

Mainline handles the screenshot size classes ASC requires:

- iPhone 6.7" (iPhone 15 Pro Max / 14 Plus)
- iPhone 6.5" (iPhone 14 Pro Max and earlier)
- iPhone 5.5" (iPhone 8 Plus era)
- iPad Pro 12.9"
- iPad Pro 11"

Check ASC's current requirements for which sizes are mandatory for your target devices.

---

## Locale management

Each project can have screenshots in multiple locales. Use **Manage Locales** within a project to add or remove languages. You can also copy a locale's screenshot set to another locale within the same project.

---

## Uploading to ASC

When your screenshots are ready:

<ol class="steps">
  <li>Open the project and tap <strong>Upload to App Store Connect</strong>.</li>
  <li>Choose the target app and version.</li>
  <li>Select which device sizes and locales to upload.</li>
  <li>Tap <strong>Upload</strong>. Mainline handles the multipart upload to ASC.</li>
</ol>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Reordering and deleting</div>
    <p>
      You can reorder screenshots within a slot by dragging, and delete individual images with a swipe. Changes are applied to ASC immediately on each action.
    </p>
  </div>
</div>

---

## Preview videos

Preview video upload is not yet supported in Mainline. Video previews can be managed via App Store Connect in the browser.

---

## Duplicating projects

Tap **Duplicate** on any project to make a copy. Useful when you're starting a new version that needs mostly the same screenshots with minor updates.
