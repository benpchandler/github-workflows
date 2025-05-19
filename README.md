# GitHub Workflows

Centralized GitHub Actions workflows for reuse across repositories.

## Available Workflows

### map-labels-to-status.yml

Maps detailed status labels to simplified project statuses in GitHub Projects.

#### Usage

To use this workflow in your repository, create a file in `.github/workflows/` with the following content:

```yaml
name: Map Status Labels to Project Status

on:
  issues:
    types: [labeled, unlabeled]
  pull_request:
    types: [labeled, unlabeled]

jobs:
  map-status:
    if: startsWith(github.event.label.name, 'status:')
    uses: benpchandler/github-workflows/.github/workflows/map-labels-to-status.yml@main
    with:
      project-id: "PVT_kwHOACOm0c4A1kb2"  # Replace with your project ID
      status-field-id: "PVTSSF_lAHOACOm0c4A1kb2zgrBHPI"  # Replace with your status field ID
```

#### Configuration

You'll need to update the following values in your workflow file:

1. `project-id`: The ID of your GitHub Project
2. `status-field-id`: The ID of the Status field in your GitHub Project

The workflow maps status labels to project statuses as follows:

| Status Label | Project Status |
|--------------|---------------|
| status:s0-backlog | Backlog |
| status:s1-prioritized, status:s2-scoped, status:s3-ready-for-dev, status:needs-design | To Do |
| status:s4-in-development, status:needs-input | In Progress |
| status:s5-needs-code-review, status:s6-revisions-requested | Review |
| status:s7-approved-for-merge, status:s8-merged | Done |
| status:blocked | Blocked |
