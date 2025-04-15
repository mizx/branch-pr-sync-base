# Branch PR Sync Base

A reusable GitHub Action to sync branches from a specified base branch (e.g., `main`) into open PRs. Useful for keeping PR branches up-to-date with the latest changes from your base branch.

## Inputs

| Input               | Type    | Default        | Description                                                 |
|---------------------|---------|----------------|-------------------------------------------------------------|
| `dry_run`           | `boolean`| `'false'`        | If true, logs actions without performing the merge/push.    |
| `base_branch`       | `string` | `'main'`       | The target base branch for PRs (e.g., `main`, `develop`).   |
| `require_auto_merge`| `boolean`| `'true'`         | Only sync PRs with auto-merge enabled.                      |
| `author_name`       | `string` | `'github-actions'` | Git author name for the commit.                             |
| `author_email`      | `string` | `'github-actions@github.com'` | Git author email for the commit.  |
| `commit_message`    | `string` | _Not defined_ | Custom commit message for the merge commit. If not provided, Git will use its default merge commit message. |

## Example Usage

```yaml
name: Sync PRs when base branch updates

on:
  push:
    branches:
      - main  # Change to your base branch name

jobs:
  sync:
    uses: your-username/branch-pr-sync-base@main
    permissions:
      contents: write
      pull-requests: write
    with:
      base_branch: main
      require_auto_merge: true
```