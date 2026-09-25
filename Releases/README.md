# Ventara update files

Ventara checks this folder directly from the `main` branch.

The version used for update comparison is stored in `release.json`:

```json
{
  "version": "1.2.0"
}
```

You normally should not edit `release.json` by hand. Set the version locally in `Ventara Generator/Version`, run the platform build scripts, then copy the generated `Ventara Generator/Output/release.json` here.

## Layout

```text
Releases/
├── release.json
├── Windows/
├── Mac/
└── Linux/
```

### Windows

Copy the **contents** of:

```text
Ventara Generator/Output/Windows/Portable/
```

into:

```text
Releases/Windows/
```

Do not copy the `Portable` wrapper folder itself.

The Windows installer from `Output/Windows/Installer` is not used by the automatic updater. Attach it to a normal GitHub Release instead.

### macOS

Copy the contents of `Ventara Generator/Output/Mac` into `Releases/Mac`.

### Linux

Copy the contents of `Ventara Generator/Output/Linux` into `Releases/Linux`.

Always copy the generated `Output/release.json` to `Releases/release.json` after building the platforms for a release. The manifest contains the version, platform file list, sizes and SHA-256 hashes Ventara uses to verify downloads.
