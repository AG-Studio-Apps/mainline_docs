---
layout: manual
title: "CI Runs"
description: "Trigger GitHub Actions workflows and monitor live run logs from Mainline."
breadcrumb: true
permalink: /manual/ci-runs/
---

<div class="page-header">
  <div class="page-header__eyebrow">User Manual</div>
  <h1>CI Runs</h1>
  <p>Trigger GitHub Actions workflows and watch live logs from your iPhone.</p>
</div>

<!-- SCREENSHOT: ci-runs-list -->
<div class="screenshot-placeholder">
  <span class="ph-icon">⚙️</span>
  <span class="ph-label">CI runs list — recent workflow runs with status</span>
  <span class="ph-hint"><!-- SCREENSHOT: ci-runs-list-view --></span>
</div>

## Requirements

CI features require a connected GitHub Personal Access Token with `repo` and `workflow` scopes. See [Onboarding — Step 2]({{ '/onboarding/' | relative_url }}#step-2--connect-github-optional) for setup.

The app's repository must be set in the App Detail view (a "Connect GitHub" row appears if it isn't).

---

## CI Runs section

The **CI Runs** section on the App Detail view shows the most recent runs for the app's linked repository. Each row shows:

- Workflow name
- Branch
- Run status (queued, in progress, success, failure, cancelled)
- Triggered time

Tap any run to open the **live monitor** for that run.

---

## Live run monitor

The run monitor shows:

- Current overall status (with a live spinner if the run is in progress)
- Each job within the workflow, with its status
- Tap a job to expand and read its step-by-step log output in real time

Mainline polls for updates automatically while the sheet is open.

---

## Triggering a workflow

You'll usually want to trigger a build after Mainline has changed something the app bundle depends on but didn't itself commit any source code — for example, after renewing a certificate, rotating a provisioning profile, or updating App Store metadata that doesn't fork a new build (description, keywords, what's-new, screenshots).

<ol class="steps">
  <li>In the App Detail view, tap <strong>Trigger Build</strong>.</li>
  <li>Select the workflow file you want to run.</li>
  <li>Select the branch.</li>
  <li>Tap <strong>Trigger</strong>. Mainline opens the live run monitor as soon as the new run appears.</li>
</ol>

<div class="callout callout--note">
  <span class="callout__icon">ℹ️</span>
  <div class="callout__body">
    <div class="callout__title">How Mainline triggers builds</div>
    <p>
      Under the hood, Mainline first tries to <strong>rerun the most recent completed run</strong> on the selected branch — this is the cleanest path because GitHub creates a fresh run record without polluting your git history. If there's no completed run to rerun (e.g. a brand-new repository), Mainline falls back to <strong>pushing an empty commit</strong> with the message <em>"Test build"</em> — your workflow's existing <code>push</code> trigger then fires the build.
    </p>
    <p>
      You don't need <code>on: workflow_dispatch</code> in your workflow YAML — Mainline works with any workflow that has ever fired on push.
    </p>
  </div>
</div>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">When to use Trigger Build vs. pushing code</div>
    <p>
      Trigger Build is for changes Mainline made that live <em>outside</em> your Swift source — secrets, profiles, metadata. If you've edited app code, just push the commit normally; the workflow's push trigger will pick it up.
    </p>
  </div>
</div>

---

## Cleaning up build artifacts

Mainline includes a **Clean Up Builds** action that can delete old expired or superseded build records from ASC (not the GitHub run logs). This helps keep the builds list readable when you have many old builds accumulating.
