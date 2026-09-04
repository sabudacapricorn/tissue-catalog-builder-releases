# Tissue Catalog Builder Releases

This public repository is the binary-only distribution host for the Windows
Employee Edition of Tissue Catalog Builder. Application source, administrator
packages, workbooks, catalogues, debug bundles, build reports, credentials, and
customer or company data do not belong here.

## Install the Employee Edition

1. Open the [Releases page](https://github.com/sabudacapricorn/tissue-catalog-builder-releases/releases).
2. Choose the latest stable release.
3. Download exactly the versioned executable and its matching checksum
   sidecar:

   ```text
   TissueCatalogBuilder_vX.Y.Z.exe
   TissueCatalogBuilder_vX.Y.Z.exe.sha256
   ```

   Replace `X.Y.Z` with the version number shown by that release. Do not
   download an EXE from the repository's Code view or from another website.
4. Open PowerShell in the download folder and verify the pair, again replacing
   `X.Y.Z` with the downloaded version:

   ```powershell
   $version = "X.Y.Z"
   $exe = ".\TissueCatalogBuilder_v${version}.exe"
   $sidecar = "$exe.sha256"

   if (-not (Test-Path -LiteralPath $exe)) {
       throw "Executable not found: $exe"
   }
   if (-not (Test-Path -LiteralPath $sidecar)) {
       throw "Checksum sidecar not found: $sidecar"
   }

   $parts = ((Get-Content -LiteralPath $sidecar -Raw).Trim() -split "\s+")
   if ($parts.Count -lt 2) {
       throw "Invalid checksum sidecar format"
   }

   $expected = $parts[0].ToLower()
   $expectedName = $parts[-1]
   $actualName = [System.IO.Path]::GetFileName($exe)

   if ($expectedName -cne $actualName) {
       throw "Checksum sidecar names '$expectedName', not '$actualName'"
   }

   $actual = (Get-FileHash -Algorithm SHA256 -LiteralPath $exe).Hash.ToLower()
   if ($actual -ne $expected) {
       throw "SHA-256 mismatch"
   }

   "SHA-256 MATCH: $actual"
   ```

5. Close any older Tissue Catalog Builder window, then run the verified EXE.

Employees do not need Python, GitHub, or a GitHub account. Updater-aware
Employee versions check this repository anonymously after the normal GUI
opens. Offline use or a failed update check does not prevent catalogue work.

## Data source options in v2.8.0 and later

v2.8.0 adds **Odoo Live** alongside **Excel Workbooks**. Employees
can explicitly connect or refresh using their own company-provided Odoo access,
then generate catalogues with the usual workflow. Windows users can choose to
remember their key with per-user encryption. Excel remains available for
offline work, and Odoo does not connect automatically at startup.

Install the latest stable EXE from the Releases page. Company connection
details, credentials, and inventory are never distributed here.

## Historical updater bootstrap

v2.7.0 was the historical one-time updater bootstrap. It is no longer the
normal installation target.

v2.6.3 does not contain an updater and cannot discover a newer release by
itself. If an employee still uses v2.6.3, close it and give that employee the
newest stable updater-aware Employee EXE from the Releases page. Do not
intentionally install v2.7.0 first.

Existing updater-aware versions can discover, verify, and activate a newer
stable release while preserving employee profiles, remembered paths, and
Output Explorer history.

## Release organization

GitHub Releases are the authoritative download location. Each current Employee
release uses:

- an exact tag such as `vX.Y.Z`;
- the title `Tissue Catalog Builder vX.Y.Z - Employee Edition`;
- stable/latest status for a production release;
- exactly one versioned Windows EXE;
- exactly one matching `.exe.sha256` sidecar; and
- concise, non-sensitive change and limitation notes.

Drafts and prereleases are not offered by the application. GitHub automatically
shows **Source code (zip)** and **Source code (tar.gz)** links for every tag.
Those archives contain only this public repository's housekeeping content; they
are not the private Tissue Catalog Builder source or supported employee
downloads.

The public `main` branch should remain limited to this housekeeping README.
Never commit application source, administrator archives, workbooks, catalogues,
debug packages, logs, build reports, credentials, or customer/company data.

## Security and support boundary

Release executables are currently not Authenticode-signed, so Windows
SmartScreen, antivirus software, or organization policy may warn about or
block them.

A matching SHA-256 checksum proves that the downloaded EXE matches the
published release bytes. It does not independently prove publisher identity;
trust also depends on HTTPS, GitHub, and control of this repository and its
account. Download only from this repository's Releases page.

Customers do not receive this application. Employees use it to produce the
catalogue PDFs delivered through the established business workflow.
