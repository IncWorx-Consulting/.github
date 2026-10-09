# IncWorx-Consulting/.github

Shared defaults for every IncWorx repo: issue forms, the PR template and the org label set. A repo uses
these automatically unless it has its own `.github/ISSUE_TEMPLATE` folder or PR template, so **don't add
those to a repo** unless it truly needs something different. Issues and code never live here.

## The flow

| What | Where | Values |
|---|---|---|
| Kind of work | Issue **type** (org setting) | Epic, Story, Task, Bug (Feature is legacy) |
| Status, release, priority, size | Fields on the org **Project** (private) | Status: Backlog, Ready, In progress, In review, Testing, Done |
| Area and flags | **Labels** (`labels.yml` here + the repo's own `.github/labels.yml` for `area:*`) | `compliance`, `financial`, `security`, `blocked`, `needs-decision` |

- An **Epic** groups Stories and Tasks as sub-issues.
- A **Story** says what a user needs and how we'll know it works (acceptance criteria as checkboxes). Testers tick them.
- A PR says `Closes #n`, so every change traces back to the issue that asked for it.

## New repo checklist

1. Link the repo to the org Project and add its open issues.
2. Optionally add `.github/labels.yml` with the repo's `area:*` labels, add the workflow below, and run it once.

```yaml
# .github/workflows/labels.yml
name: Labels
on:
  workflow_dispatch:
  push:
    branches: [main]
    paths: ['.github/labels.yml']
jobs:
  sync:
    uses: IncWorx-Consulting/.github/.github/workflows/sync-labels.yml@main
```
