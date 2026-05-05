---
layout: manual
title: "TestFlight Builds"
description: "View your TestFlight builds, edit What to Test notes, and schedule releases in Mainline."
breadcrumb: true
permalink: /mainline_docs/manual/testflight/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>TestFlight Builds</h1>
  <p>View builds, edit What to Test notes, and schedule your release — without opening App Store Connect.</p>
</div>

<!-- SCREENSHOT: testflight-builds-list -->
<div class="screenshot-placeholder">
  <span class="ph-icon">🛫</span>
  <span class="ph-label">Builds list view</span>
  <span class="ph-hint"><!-- SCREENSHOT: testflight-builds-list --></span>
</div>

## Builds section

The **Builds** section on the App Detail view shows all TestFlight builds for the current app version, with status indicators: processing, ready to submit, expired, invalid, and so on.

Tap a build to open the **Build Detail** view.

---

## Build detail

Each build's detail view shows:

- **Version and build number**
- **Processing status** — Mainline shows a banner if a build is still being processed by ASC
- **What to Test** notes — editable directly in Mainline
- **Build expiry** date
- **Attached version** — the app version this build is associated with

### Editing What to Test

<ol class="steps">
  <li>Tap a build to open its detail.</li>
  <li>Tap <strong>What to Test</strong>.</li>
  <li>Edit the text (no character limit enforced by ASC, but keep it concise).</li>
  <li>Tap <strong>Save</strong>. Changes are sent to ASC immediately.</li>
</ol>

---

## Attaching a build to a version

Before submitting for review, you need a build attached to your editable version. In the **Builds** section:

<ol class="steps">
  <li>Tap <strong>Pick Build</strong> (shown when no build is attached to the current version).</li>
  <li>Choose the build you want to submit.</li>
  <li>Confirm. The build is attached and the Submission section updates to reflect it.</li>
</ol>

---

## Scheduling a release

For builds that are ready for release (approved by App Store review), Mainline supports scheduling:

<ol class="steps">
  <li>Open the <strong>Submission</strong> section for the current version.</li>
  <li>Tap <strong>Schedule Release</strong>.</li>
  <li>Choose a release date and time.</li>
  <li>Save. The scheduled date is set in ASC; the version will release automatically at that time.</li>
</ol>

You can update or clear the scheduled date before it fires.

---

## Beta group and tester management

Beta group management (adding/removing testers, creating beta groups) is handled via the official TestFlight section of App Store Connect. Mainline focuses on the build-management and metadata side of TestFlight rather than duplicating the tester management flow that ASC's own iOS app handles well.

---

## Common pitfalls

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Processing builds can take 10–30 minutes</div>
    <p>
      After uploading a build with Xcode or CI, it takes time for ASC to finish processing. During this window, the build shows a "Processing" status and cannot be attached to a version or submitted. Mainline refreshes the build list automatically, but you may need to wait.
    </p>
  </div>
</div>
