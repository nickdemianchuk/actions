# actions

Reusable GitHub Actions workflows: commit/PR linting, semantic-release versioning, and Terraform Cloud plan/apply.

## Workflows

| Workflow | Trigger | Purpose |
|---|---|---|
| [`lint-pr.yml`](#lint-pryml) | `pull_request` | Lint PR title against the [semantic-release](https://semantic-release.org) commit convention |
| [`lint-commits.yml`](#lint-commitsyml) | `push` | Lint commits against the [semantic-release](https://semantic-release.org) commit convention |
| [`release.yml`](#releaseyml) | `workflow_call` | semantic-release: version, changelog, tag, GitHub release |
| [`tf-plan.yml`](#tf-planyml) | `workflow_call` | `terraform plan` on a Terraform Cloud workspace |
| [`tf-apply.yml`](#tf-applyyml) | `workflow_call` | `terraform apply` on a Terraform Cloud workspace |

### `lint-pr.yml`
Lints the PR title against the commit convention [semantic-release](https://semantic-release.org) expects (Angular preset, scope required). Must be triggered by a `pull_request` event.

```yaml
jobs:
  lint-pr:
    uses: nickdemianchuk/actions/.github/workflows/lint-pr.yml@main
```

### `lint-commits.yml`
Lints every commit subject on the branch (`origin/main..HEAD`) against the commit convention [semantic-release](https://semantic-release.org) expects (Angular preset, scope required). Must be triggered by a `push` event.

```yaml
jobs:
  lint-commits:
    uses: nickdemianchuk/actions/.github/workflows/lint-commits.yml@main
```

### `release.yml`
Runs [semantic-release](https://semantic-release.org) on `main`: bumps the version from commit history, updates `CHANGELOG.md`, tags, and publishes a GitHub release.

```yaml
jobs:
  release:
    permissions:
      contents: write
      issues: write
      pull-requests: write
    uses: nickdemianchuk/actions/.github/workflows/release.yml@main
    secrets:
      APP_CLIENT_ID: ${{ vars.OCTO_BUDDY_CLIENT_ID }}
      APP_PRIVATE_KEY: ${{ secrets.OCTO_BUDDY_PRIVATE_KEY }}
```

`APP_CLIENT_ID`/`APP_PRIVATE_KEY` mint a short-lived [Octo Buddy](https://github.com/apps/octo-buddy) GitHub App token (via `actions/create-github-app-token`) so release commits push and trigger downstream workflows, in place of a stored PAT. The app is registered per-repo in `github-ops`; see that repo's README for setup.

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
      TF_GITHUB_TOKEN: ${{ secrets.TF_GITHUB_TOKEN }}
      TF_VAR_octo_buddy_private_key: ${{ secrets.OCTO_BUDDY_PRIVATE_KEY }}
```

`TF_VAR_octo_buddy_private_key` passes the [Octo Buddy](https://github.com/apps/octo-buddy) app's private key through to `github-ops`'s Terraform config as `octo_buddy_private_key`.

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
      TF_VAR_octo_buddy_private_key: ${{ secrets.OCTO_BUDDY_PRIVATE_KEY }}
```

`TF_VAR_octo_buddy_private_key` passes the [Octo Buddy](https://github.com/apps/octo-buddy) app's private key through to `github-ops`'s Terraform config as `octo_buddy_private_key`.

## Versioning

`@main` always tracks the latest version. Pin to a tag (e.g. `@0.3.3`) or commit SHA instead for reproducible builds.
