---
layout: manual
title: "Submission"
description: "Submit your app for review, manage phased release, and handle rejections — all from Mainline."
breadcrumb: true
permalink: /mainline_docs/manual/submission/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>Submission</h1>
  <p>Submit for review, control phased rollouts, and respond to rejections — without opening a browser.</p>
</div>

<!-- SCREENSHOT: submission-section -->
<div class="screenshot-placeholder">
  <span class="ph-icon">🚀</span>
  <span class="ph-label">Submission section — review status and actions</span>
  <span class="ph-hint"><!-- SCREENSHOT: submission-section-view --></span>
</div>

## The Submission section

The **Submission** section at the bottom of the App Detail view tracks your current version's lifecycle:

- **Version state** — Prepare for Submission, Waiting for Review, In Review, Approved, Ready for Sale, etc.
- **Attached build** — which build is associated with this version
- **Phased release status** — if you've enabled a phased rollout
- **Rejection details** — if Apple has rejected the version, the reason is shown inline

---

## Submitting for review

<ol class="steps">
  <li>Make sure you have an <strong>editable version</strong> and a <strong>build attached</strong> to it.</li>
  <li>Tap <strong>Submit for Review</strong>.</li>
  <li>The pre-flight checklist appears. It checks for common issues: missing metadata fields, missing screenshots, no attached build, age rating not set. Each item shows a pass or warning.</li>
  <li>Fill in any required <strong>Review Information</strong> — reviewer notes, demo account credentials if your app requires login, and any other notes for the App Store reviewer.</li>
  <li>Select your <strong>release preference</strong>: Manual release (you release after approval), Automatic release (releases as soon as approved), or Scheduled release (releases at a specific date/time).</li>
  <li>Tap <strong>Submit</strong>. The submission is sent to ASC.</li>
</ol>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Review information is saved</div>
    <p>
      Reviewer notes and demo credentials are stored in ASC for the version. You can copy them from your previous version using <strong>Copy Review Info</strong> when starting a new version.
    </p>
  </div>
</div>

---

## Creating a new version

When your app is live (or you have no version in Prepare for Submission state), tap **New Version** to create a new version record in ASC:

- Enter the new version number (e.g. `1.1.0`)
- Choose the platform
- Optionally copy metadata (listing copy, screenshots, review details) from the live version

Alternatively, use **Start Next Version Wizard** after a version goes live. This wizard offers to copy all metadata from the live version and pre-populate What's New from your previous What's New text.

---

## Phased release

Phased release lets you roll out an approved update to a percentage of eligible users over 7 days, rather than all at once. Mainline's phased-release controls are in the Submission section:

| Action | When available |
|---|---|
| **Pause phased release** | While the rollout is active |
| **Resume phased release** | While paused |
| **Release to all users** | At any point during the rollout (pushes to 100%) |
| **Cancel phased release** | Removes the rollout — the version stays live |

Phased release is enabled when submitting for review (a toggle in the Submit sheet).

---

## Handling rejections

If Apple rejects your version, the rejection reason appears directly in the Submission section. You can:

- **Read the full rejection message** in-app
- **Edit** the relevant fields (metadata, screenshots, review info)
- **Resubmit** once you've addressed the issues

---

## Cancelling a submission

If you need to pull back a submission (e.g. you uploaded the wrong build), tap **Cancel Submission** while the version is in "Waiting for Review" state. You can then make changes and resubmit.

<div class="callout callout--warn">
  <span class="callout__icon">⚠️</span>
  <div class="callout__body">
    <div class="callout__title">Cannot cancel once "In Review"</div>
    <p>
      Once Apple has started reviewing your app, the Cancel Submission action is no longer available. You'd need to contact App Store Review directly if there's a critical issue.
    </p>
  </div>
</div>
