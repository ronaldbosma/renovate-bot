# Renovate Bot

This repository runs a self-hosted Renovate bot on a schedule to scan other GitHub repositories and open pull requests for dependency updates, including Bicep modules (which is currently not supported by Dependabot).

## How it works

- A GitHub Actions workflow runs on the first day of each month and on manual dispatch.
- The workflow executes Renovate against a list of target repositories.
- Renovate uses the config in [.github/renovate-config.json](.github/renovate-config.json).

## Setup

1. Create a Personal Access Token on the account that should author PRs. 
   See https://docs.renovatebot.com/modules/platform/github/
2. Add the token as a repository secret in this repo:
   - Settings → Secrets and variables → Actions → New repository secret
   - Name: `RENOVATE_TOKEN`  Value: your PAT
3. Update the target repositories list in the `repositories` property in:
   - File: [.github/renovate-config.json](.github/renovate-config.json)
   - Format is a JSON array of `"owner/repo"` strings.
4. (Optional) Adjust the schedule/cron or timezone window in [.github/workflows/renovate.yml](.github/workflows/renovate.yml) if needed.

## Add more repositories

Edit [.github/renovate-config.json](.github/renovate-config.json) and add the repository to the `repositories` property. Use format: `"owner/repo"`

## Notes

- Labels `dependencies` and `renovate` are applied to PRs for easier filtering.
- The workflow uses the PAT (`RENOVATE_TOKEN`) for all operations; the built-in `GITHUB_TOKEN` is not used.