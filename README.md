# NeonTowel's Community Packages Scoop Bucket

[![Tests](https://github.com/NeonTowel/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/NeonTowel/scoop-bucket/actions/workflows/ci.yml) [![Excavator](https://github.com/NeonTowel/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/NeonTowel/scoop-bucket/actions/workflows/excavator.yml)

Welcome to NeonTowel's community Scoop bucket repository! This repository hosts a collection of community-contributed packages for the [Scoop](https://scoop.sh) Windows command-line installer. The first package available is Royal TS.

## Installation

To add this bucket to your Scoop installation and install Royal TS, run the following commands in PowerShell:

```pwsh
scoop bucket add neontowel https://github.com/NeonTowel/scoop-bucket
scoop install neontowel/royal-ts
```

## Contributing

We welcome contributions to expand the list of available packages. To contribute:

1. Fork the repository and clone it locally.
2. Create a new manifest by copying `bucket/app-name.json.template` to `bucket/<app-name>.json`.
3. Fill in the manifest details according to the [App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests) guide.
4. Commit your changes and push them to your fork.
5. Open a pull request with a clear description of your changes.

Please ensure you have read the [Contributing Guide](https://github.com/ScoopInstaller/.github/blob/main/.github/CONTRIBUTING.md) before submitting your pull request.

## Update manifests

To update a single manifest with latest versions, you can use the checkver.ps1 script:

```pwsh
.\bin\checkver.ps1 royal-ts -Update
```

This will update the manifest with the latest version and hash.

To update all manifests, you can use the following command:

```pwsh
.\bin\checkver.ps1 -Update
```

Ensure the manifests contain the `autoupdate` section, see [App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests) for more details.

## Support

For any questions or support, please visit the [Scoop Community Support](https://github.com/ScoopInstaller/Scoop/discussions) page.

## License

This project is licensed under the [Unlicense](LICENSE), which means it is free and unencumbered software released into the public domain.
