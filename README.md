# Tissue Catalog Builder Releases

This public repository is the binary-only distribution host for the Windows
Employee Edition of Tissue Catalog Builder. Application source, administrator
packages, workbooks, catalogues, debug bundles, build reports, credentials, and
customer or company data do not belong here.

## Install the Employee Edition

1. Open the [Releases page](https://github.com/sabudacapricorn/tissue-catalog-builder-releases/releases).
2. Choose the latest stable release.
3. Download exactly the versioned executable and its matching checksum, for
   example:

   ```text
   TissueCatalogBuilder_v2.7.0.exe
   TissueCatalogBuilder_v2.7.0.exe.sha256
   ```

4. Verify the checksum in PowerShell:

   ```powershell
   $exe = ".\TissueCatalogBuilder_v2.7.0.exe"
   $expected = (Get-Content "$exe.sha256").Split()[0].ToLower()
   $actual = (Get-FileHash -Algorithm SHA256 $exe).Hash.ToLower()
   if ($actual -ne $expected) { throw "SHA-256 mismatch" } else { "SHA-256 MATCH: $actual" }
   ```

5. Close any older Tissue Catalog Builder window, then run the verified EXE.

v2.7.0 is the one-time updater bootstrap. v2.6.3 does not contain an updater,
so employees must receive and launch v2.7.0 manually once. Updater-aware
Employee versions check this repository anonymously after the normal GUI opens;
employees do not need GitHub accounts. Offline or failed checks do not prevent
normal application use.

## Release organization

GitHub Releases are the authoritative download location. Each release uses:

- an exact tag such as `v2.7.0`;
- a descriptive title identifying stable, bootstrap, or legacy status;
- one exact versioned Windows EXE;
- one matching `.exe.sha256` sidecar;
- concise installation, change, and limitation notes.

Drafts and prereleases are not offered by the application. Source archives
automatically shown by GitHub contain only this public repository's housekeeping
content, not the private application source.

## Security and support boundary

Release executables are currently not Authenticode-signed, so Windows
SmartScreen or organization policy may warn about them. A matching SHA-256
checksum detects changed bytes but does not independently prove publisher
identity; download only from this repository's Releases page.

Customers do not receive this application. Employees use it to produce the
catalogue PDFs that are delivered through the established business workflow.
