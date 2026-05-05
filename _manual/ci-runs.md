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

<ol class="steps">
  <li>In the App Detail view, tap <strong>Trigger Build</strong> (or the equivalent button shown in the CI section).</li>
  <li>Select the workflow file you want to run (Mainline lists all workflow files in your repo's <code>.github/workflows/</code> folder that have <code>workflow_dispatch</code> enabled).</li>
  <li>Select the branch to run on.</li>
  <li>Tap <strong>Trigger</strong>. Mainline dispatches the workflow via the GitHub API and immediately opens the run monitor for the new run.</li>
</ol>

<div class="callout callout--tip">
  <span class="callout__icon">💡</span>
  <div class="callout__body">
    <div class="callout__title">Only <code>workflow_dispatch</code> workflows can be triggered</div>
    <p>
      GitHub requires workflows to have <code>on: workflow_dispatch</code> in their YAML to be manually triggered. If no workflows appear in the list, add the <code>workflow_dispatch</code> trigger to your workflow file and push the change.
    </p>
  </div>
</div>

---

## Cleaning up build artifacts

Mainline includes a **Clean Up Builds** action that can delete old expired or superseded build records from ASC (not the GitHub run logs). This helps keep the builds list readable when you have many old builds accumulating.
