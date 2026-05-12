This file provides guidance to AI coding agents and assistants when working with code in this repository.

## What This Repo Is

A [Scoop](https://scoop.sh) bucket — a collection of JSON app manifests for the Windows CLI package manager. Each file in `bucket/` describes how to download, install, and auto-update one application.

## Manifest Schema

Every `bucket/<app-name>.json` must follow the Scoop manifest format. Required fields:

- `version` — current version string
- `description` — short app description
- `homepage` — app's website
- `license` — SPDX identifier or `"Proprietary"`
- `architecture` — nested by `64bit`/`32bit`, each with `url` and `hash` (SHA256)
- `checkver` — how Scoop detects the latest version (URL + regex or jsonpath)
- `autoupdate` — URL template using `$version` to auto-generate the updated download URL

Optional but common:
- `bin` — executable(s) to add to PATH
- `shortcuts` — Start Menu entries: `[["exe", "display name"]]`
- `persist` — paths to preserve across updates (user data, config)
- `post_install` — PowerShell lines run after extraction (array of strings, not a script block)
- `innosetup: true` — set when the installer is InnoSetup-based; pair with `extract_dir: "{code_GetDestDir}"`

Hash value must be lowercase SHA256. Use `bin/checkhashes.ps1 <app-name>` to verify or regenerate hashes.

## Scripts in `bin/`

All scripts delegate to Scoop's own tooling via `$env:SCOOP_HOME`. Run them from the repo root.

| Script | Purpose |
|---|---|
| `bin/checkver.ps1 <app> -Update` | Update a single manifest to latest version |
| `bin/checkver.ps1 -Update` | Update all manifests |
| `bin/checkhashes.ps1` | Verify/regenerate download hashes |
| `bin/checkurls.ps1` | Validate that all download URLs are reachable |
| `bin/formatjson.ps1` | Format all JSON manifests (4-space indent, CRLF) |
| `bin/test.ps1` | Run the Pester test suite |

## Running Tests

Tests require Scoop installed locally (sets `$env:SCOOP_HOME`) plus `BuildHelpers` and `Pester >= 5.2.0`:

```pwsh
# Run all tests
$env:SCOOP_HOME = Convert-Path (scoop prefix scoop)
.\bin\test.ps1
```

Tests are defined in `Scoop-Bucket.Tests.ps1` and use Scoop's shared `Import-Bucket-Tests.ps1` — they validate JSON syntax, required fields, URL reachability, and hash correctness for every manifest in `bucket/`.

## Formatting Rules

- JSON manifests: 4-space indent, CRLF line endings, UTF-8, trailing newline
- YAML files: 2-space indent
- Run `bin/formatjson.ps1` before committing new or updated manifests

## Adding a New Manifest

1. Create `bucket/<app-name>.json` following the schema above.
2. Include both `checkver` and `autoupdate` sections so Excavator can maintain it.
3. Run `bin/checkhashes.ps1 <app-name>` to verify the hash.
4. Run `bin/checkurls.ps1 <app-name>` to confirm the URL is reachable.
5. Run `bin/test.ps1` to pass the full test suite.
6. Run `bin/formatjson.ps1` to normalize formatting.

## Automation

- **Excavator** runs every 4 hours via GitHub Actions and auto-updates manifests that have `checkver`/`autoupdate` configured, opening PRs for each change.
- **CI** runs on every push and PR, testing both `powershell` (Windows PowerShell 5.1) and `pwsh` (PowerShell 7+).

## Scoop Manifest Reference

Full field documentation: <https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests>
