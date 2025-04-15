# Branch PR Sync Base

A reusable GitHub Action to sync branches from a specified base branch (e.g., `main`) into open PRs. Useful for keeping PR branches up-to-date with the latest changes from your base branch.

## Inputs

| Input               | Type      | Default        | Description                                                 |
|---------------------|-----------|----------------|-------------------------------------------------------------|
| `github_token`      | `string`  | _Required_     | GitHub token for authentication. Typically passed as `${{ secrets.GITHUB_TOKEN }}`. |
| `dry_run`           | `boolean` | `'false'`      | If true, logs actions without performing the merge or push. Useful for testing. |
| `base_branch`       | `string`  | `'main'`       | The target base branch for PRs (e.g., `main`, `develop`).   |
| `require_auto_merge`| `boolean` | `'true'`       | Only sync PRs with auto-merge enabled.                      |
| `author_name`       | `string`  | `'github-actions'` | Git author name for the commit.                             |
| `author_email`      | `string`  | `'github-actions@github.com'` | Git author email for the commit.  |
| `commit_message`    | `string`  | _Not defined_  | Custom commit message for the merge commit. If not provided, Git will use its default merge commit message. |

## Example Usage

```yaml
name: Sync PRs when base branch updates

on:
  push:
    branches:
      - main  # Change to your base branch name

jobs:
  sync:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Use Branch PR Sync Base Action
        uses: mizx/branch-pr-sync-base@v1
        with:
          base_branch: main
          require_auto_merge: true
          github_token: ${{ secrets.GITHUB_TOKEN }}
```
