# Versioned Releases and Zenodo Archival

## What the workflow does

The [Publish versioned release workflow](.github/workflows/release.yml) is manually triggered from GitHub Actions on `main`. It:

1. Requires a semantic version such as `0.1.2` and verifies that it matches `CITATION.cff` and the top release section in `CHANGELOG.md`.
2. Refreshes `metadata/SHA256SUMS.txt` over the tracked publication files and verifies every checksum.
3. Creates an annotated tag (`v0.1.2`) and publishes a GitHub Release with changelog-based notes. A custom title can be supplied.
4. Uses a token owned by the GitHub account that should appear as the release author.

It does not alter the core specification or publish to Zenodo through a separate API call.

## One-time GitHub setup

To make releases appear as published by your GitHub account rather than `github-actions[bot]`:

1. In GitHub, create a fine-grained personal access token owned by your account, scoped only to this repository, with **Contents: Read and write** permission.
2. Open this repository's **Settings → Secrets and variables → Actions**.
3. Add a repository secret named `RELEASE_TOKEN` and paste the token there. Never commit a token to the repository or share it in chat.

The workflow deliberately fails before checkout or publication if `RELEASE_TOKEN` is missing. The Release author is the account that owns this token. The workflow also commits a refreshed checksum manifest under that authenticated identity only when the manifest needs updating.

## Publish a version

1. Ensure the new version exists in both `CITATION.cff` and `CHANGELOG.md`.
2. Open **Actions → Publish versioned release → Run workflow** and select the `main` branch.
3. Enter the version without the leading `v` (for this release, `0.1.2`). Choose whether it is a pre-release.
4. Wait for the run to complete, then verify the release under the repository's **Releases** page.

The workflow uses an annotated Git tag and changelog-based release notes. It refuses to overwrite an existing release. If a prior run pushed a tag but failed before publishing the release, re-running the same version can finish the release if the tag already points to a matching versioned commit.

## One-time Zenodo setup

No Zenodo token is required when using Zenodo's official GitHub integration.

1. Sign in to Zenodo and open the profile menu's **GitHub** page.
2. Use **Sync now** if needed, find this repository, and enable its toggle.
3. After publishing a GitHub Release, check that release's processing status and DOI in the Zenodo GitHub page.

Zenodo automatically archives future GitHub releases only after the repository is enabled. If the integration was not enabled at release time, do not assume that older releases will be archived retroactively. Each successfully archived version receives its own version DOI; the concept DOI linked from the repository points to the latest version.

## Current publication readiness

**Do not run the publication workflow for this research revision yet.** The Component Contract and prior-art analysis are a working draft, and `LNASF-v0.2-draft.tex` has not yet been compiled, visually checked, or reconciled with a final publication PDF. The Version 0.1 PDF remains a historical snapshot. Before publishing, finish the full-text prior-art comparison and evaluation, compile and inspect the revised PDF, update all citation/version metadata, and regenerate the checksum manifest in the release workflow. A workflow file or planned version is not evidence of a completed release.
