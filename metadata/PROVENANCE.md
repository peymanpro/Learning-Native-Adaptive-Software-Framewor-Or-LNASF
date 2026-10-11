# Publication Provenance Notes

The repository preserves the earlier Version 0.1 LNASF disclosure and catalogs limited engineering examples. Version 0.2.0 is prepared to archive a research proposal formalizing the candidate LNASF Component Contract and adding a preliminary prior-art comparison. This version is not represented as a peer-reviewed paper, verified novel contribution, or empirical demonstration of improved performance. The Version 0.1 TeX/PDF remain historical snapshots; the candidate contract is described in the separate Version 0.2.0 draft source and PDF.

## Automated release path

1. Keep the repository public and enable it in the Zenodo GitHub integration.
2. Configure a repository Actions secret named `RELEASE_TOKEN` using a fine-grained token owned by the account that should publish the release. Scope it to this repository with Contents read/write permission.
3. From Actions, run **Publish versioned release** on `main` and enter the version recorded in `CITATION.cff` and `CHANGELOG.md`.
4. The workflow validates metadata, refreshes and verifies `metadata/SHA256SUMS.txt`, creates an annotated tag, and publishes a GitHub Release. It fails before changing anything if the required account-owned token is absent.
5. When Zenodo integration is enabled for this repository, Zenodo automatically ingests the new GitHub release and creates a versioned archival record. Confirm its processing and resulting DOI in the Zenodo GitHub integration page.

## Preservation notes

- Keep any eventual release tag, target commit hash, release notes, and SHA-256 manifest together.
- Before publication, compile and inspect the revised TeX source, reconcile the PDF and Markdown, verify references and metadata, and regenerate the checksum manifest from repository bytes. The current manifest is explicitly marked stale.
- Use the concept DOI for a citation to the evolving repository and a version-specific DOI when citing a particular archived release.
- If the repository is not enabled in Zenodo before a release is created, enable it before a later release; do not assume older releases will be archived retroactively.

This file documents a repeatable publication process. It is not a legal guarantee. Patent strategy and legal effect vary by jurisdiction.
