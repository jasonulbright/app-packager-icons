# app-packager-icons

This repository hosts operator-contributed icon files for the **External** icon source in
[AppPackager](https://github.com/jasonulbright/app-packager).

A packager script tagged `IconSource: External` looks for an icon at
`Packagers\Icons\<packagername>.ico` or `.png` when it stages content, where `<packagername>`
is the packager script's file name without the `package-` prefix and without the `.ps1`
extension. `package-7zip.ps1` therefore looks for `Packagers\Icons\7zip.ico` or
`Packagers\Icons\7zip.png`. When both exist, `.ico` wins. When neither exists the stage
continues without an icon.

AppPackager's Options window can download this repository's latest `icon-pack.zip` release
asset, verify it against `checksums.txt`, and extract it into `Packagers\Icons\`.

## Ownership of application artwork

Application icons are the property of their respective vendors. This repository is
community- and operator-populated: the project itself commits no vendor artwork. Anyone who
adds an icon file here is responsible for confirming they may redistribute it. Nothing in
this repository grants any right in a vendor's trademarks or artwork.

## Layout

```
icons/           icon files, named <packagername>.ico or <packagername>.png
manifest.json    pack version, minimum AppPackager version, and the icon index
```

The release asset `icon-pack.zip` is flat: `manifest.json` and every icon file sit at the
zip root, because the zip extracts directly into `Packagers\Icons\` and `Add-StageIcon`
looks for `Packagers\Icons\<packagername>.ico|png` with no intervening folder.

## manifest.json

```json
{
  "PackVersion": "1.0.0",
  "MinAppVersion": "1.5.0.0",
  "Icons": [
    { "File": "7zip.ico", "Packager": "7zip" }
  ]
}
```

| Field | Meaning |
| --- | --- |
| `PackVersion` | Version of the pack itself. Shown in the Options window status line. |
| `MinAppVersion` | Oldest AppPackager version the pack targets. A newer value than the running app produces a warning, not a refusal. |
| `Icons` | One entry per icon file. `File` is the file name inside the zip; `Packager` is the packager name the icon binds to. |

## Contributing an icon

1. Name the file after the packager (`<packagername>.ico` or `<packagername>.png`) and place
   it in `icons/`.
2. Add a matching entry to the `Icons` array in `manifest.json`.
3. Confirm you may redistribute the artwork before opening the pull request.

## License

The repository scaffolding (README, manifest schema, packaging scripts) is MIT. Individual
icon files remain the property of their respective vendors and are not covered by that
license.
