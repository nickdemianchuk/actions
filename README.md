# actions

Reusable GitHub Actions workflows: commit/PR linting, semantic-release versioning, and Terraform Cloud plan/apply.

## Workflows

| Workflow | Trigger | Purpose |
|---|---|---|
| [`lint-pr.yml`](#lint-pryml) | `pull_request` | Lint PR title against the [semantic-release](https://semantic-release.gitbook.io/semantic-release/) commit convention |
| [`lint-commits.yml`](#lint-commitsyml) | `push` | Lint commits against the [semantic-release](https://semantic-release.gitbook.io/semantic-release/) commit convention |
| [`release.yml`](#releaseyml) | `workflow_call` | semantic-release: version, changelog, tag, GitHub release |
| [`tf-plan.yml`](#tf-planyml) | `workflow_call` | `terraform plan` on a Terraform Cloud workspace |
| [`tf-apply.yml`](#tf-applyyml) | `workflow_call` | `terraform apply` on a Terraform Cloud workspace |

### `lint-pr.yml`
Lints the PR title against the commit convention [semantic-release](https://semantic-release.gitbook.io/semantic-release/) expects (Angular preset, scope required). Must be triggered by a `pull_request` event.

```yaml
jobs:
  lint-pr:
    uses: nickdemianchuk/actions/.github/workflows/lint-pr.yml@main
```

### `lint-commits.yml`
Lints every commit subject on the branch (`origin/main..HEAD`) against the commit convention [semantic-release](https://semantic-release.gitbook.io/semantic-release/) expects (Angular preset, scope required). Must be triggered by a `push` event.

```yaml
jobs:
  lint-commits:
    uses: nickdemianchuk/actions/.github/workflows/lint-commits.yml@main
```

### `release.yml`
Runs [semantic-release](https://semantic-release.gitbook.io/semantic-release/) on `main`: bumps the version from commit history, updates `CHANGELOG.md`, tags, and publishes a GitHub release. Skips runs triggered by `github-actions[bot]` to avoid loops.

```yaml
jobs:
  release:
    permissions:
      contents: write
      issues: write
      pull-requests: write
    uses: nickdemianchuk/actions/.github/workflows/release.yml@main
    secrets:
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

`GH_TOKEN` needs a token with permission to push commits/tags and create releases (a fine-grained PAT, not the default `GITHUB_TOKEN`, if you want release commits to trigger downstream workflows).

### `tf-plan.yml`
Runs `terraform plan` against a Terraform Cloud workspace via [dflook/terraform-plan](https://github.com/dflook/terraform-plan) and posts the plan as a PR comment.

```yaml
jobs:
  tf-plan:
    uses: nickdemianchuk/actions/.github/workflows/tf-plan.yml@main
    with:
      workspace: my-workspace
    secrets:
      TF_CLOUD_ORGANIZATION: ${{ secrets.TF_CLOUD_ORGANIZATION }}
      TF_API_TOKEN: ${{ secrets.TF_API_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

### `tf-apply.yml`
Runs `terraform apply` (auto-approved) against a Terraform Cloud workspace via [dflook/terraform-apply](https://github.com/dflook/terraform-apply).

```yaml
jobs:
  tf-apply:
    uses: nickdemianchuk/actions/.github/workflows/tf-apply.yml@main
    with:
      workspace: my-workspace
    secrets:
      TF_CLOUD_ORGANIZATION: ${{ secrets.TF_CLOUD_ORGANIZATION }}
      TF_API_TOKEN: ${{ secrets.TF_API_TOKEN }}
      TF_GITHUB_TOKEN: ${{ secrets.TF_GITHUB_TOKEN }}
```

## Versioning

`@main` always tracks the latest version. Pin to a tag (e.g. `@0.3.3`) or commit SHA instead for reproducible builds.
