# NeonTowel's Community Scoop Bucket

[![Tests](https://github.com/NeonTowel/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/NeonTowel/scoop-bucket/actions/workflows/ci.yml) [![Excavator](https://github.com/NeonTowel/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/NeonTowel/scoop-bucket/actions/workflows/excavator.yml)

A community [Scoop](https://scoop.sh) bucket with a curated set of Windows applications not available in the official buckets.

## Installation

```pwsh
scoop bucket add neontowel https://github.com/NeonTowel/scoop-bucket
scoop install neontowel/<app-name>
```

## Available Packages

| Package | Description |
|---|---|
| `azure-cli` | Azure command-line interface |
| `awesome-git` | Git GUI client |
| `chatbox` | Desktop AI chat client |
| `cursor` | AI-first code editor based on VSCode |
| `faraday` | Collaborative penetration testing platform |
| `fancywm` | Dynamic tiling window manager for Windows |
| `gum` | Glamorous shell script utilities |
| `heroic` | Open source Epic Games and GOG launcher |
| `ipcalc-go` | IP address calculator |
| `neo-codium` | VSCodium with custom extensions |
| `omt` | Oh My Tools |
| `rose-pine-cursor` | Rosé Pine cursor theme |
| `royal-ts` | Remote management solution (RDP, SSH, VNC) |
| `see-through-windows-ng` | Make windows transparent |
| `seethroughwindows` | Make windows transparent |
| `seethroughwindows-beta` | Beta builds of SeeThroughWindows |
| `startctl` | Windows Start menu controller |
| `vscode` | Visual Studio Code |

## Update Manifests

Update a single manifest to its latest version:

```pwsh
.\bin\checkver.ps1 <app-name> -Update
```

Update all manifests at once:

```pwsh
.\bin\checkver.ps1 -Update
```

Verify download URLs are reachable:

```pwsh
.\bin\checkurls.ps1
```

Verify or regenerate SHA256 hashes:

```pwsh
.\bin\checkhashes.ps1
```

Format all manifests (run before committing):

```pwsh
.\bin\formatjson.ps1
```

## Contributing

1. Fork the repository and clone it locally.
2. Create `bucket/<app-name>.json` following the [App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests) guide.
3. Include `checkver` and `autoupdate` sections so the manifest stays current automatically.
4. Run `.\bin\checkhashes.ps1 <app-name>` and `.\bin\checkurls.ps1 <app-name>` to validate.
5. Run `.\bin\test.ps1` to pass the full test suite (requires Scoop, `BuildHelpers`, and `Pester >= 5.2.0`).
6. Run `.\bin\formatjson.ps1` to normalize JSON formatting.
7. Open a pull request with a description of the new or changed package.

Please read the [Contributing Guide](https://github.com/ScoopInstaller/.github/blob/main/.github/CONTRIBUTING.md) before submitting a pull request.

## Automation

Manifests with `checkver` and `autoupdate` sections are updated automatically every 4 hours by [Excavator](https://github.com/ScoopInstaller/GithubActions), which opens PRs for any new versions it finds.

## License

[Unlicense](LICENSE) — public domain.
