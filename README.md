# Ventara

Official Ventara download and update endpoint.

This public repository intentionally contains **no Ventara application source code**. The newest compiled Ventara version is published on the **Releases** page and is also used by Ventara's built-in updater.

## What the GitHub repository itself should look like

Keep the normal repository extremely small. You do **not** upload the Ventara project, Electron source, `desktop` folder, tests, Node modules, or build tools here.

```text
DylNETGroup/Ventara/
├── README.md
└── PUBLISH-UPDATE.txt
```

The actual Ventara downloads live under **GitHub Releases**, not as files/folders committed into the repository.

## Example GitHub layout

For example, while Ventara 1.0.1 is the current version, GitHub would effectively look like this:

```text
DylNETGroup/Ventara
│
├── README.md
├── PUBLISH-UPDATE.txt
│
└── Releases
    └── Ventara v1.0.1
        └── Assets
            ├── Ventara-1.0.1-win-x64.exe
            ├── Ventara-1.0.1-win-x64.exe.blockmap
            ├── Ventara-1.0.1-Windows-Portable.exe
            ├── latest.yml
            │
            ├── Ventara-1.0.1-mac-universal.dmg
            ├── Ventara-1.0.1-mac-universal.zip
            ├── Ventara-1.0.1-mac-universal.zip.blockmap
            ├── latest-mac.yml
            │
            ├── Ventara-1.0.1-linux-x64.AppImage
            ├── Ventara-1.0.1-linux-arm64.AppImage
            └── latest-linux.yml
```

The exact filenames can vary slightly depending on the current Electron Builder configuration. The important rule is: **upload the generated files exactly as Ventara Generator produced them; do not rename the update manifests or blockmap files.**

## Where those files come from

On your development machine, Ventara Generator keeps the latest compiled output here:

```text
Ventara Generator/
└── Output/
    ├── Windows/
    │   └── latest Windows build files
    ├── macOS/
    │   └── latest macOS build files
    ├── Linux/
    │   └── latest Linux build files
    │
    ├── GitHub Update/
    │   ├── Windows installer/update files
    │   ├── Windows Portable build
    │   ├── macOS DMG/ZIP/update files
    │   ├── Linux AppImages/update files
    │   ├── latest.yml
    │   ├── latest-mac.yml
    │   └── latest-linux*.yml
    │
    ├── CURRENT-VERSION.txt
    └── PUBLISH-LATEST.txt
```

For GitHub, the folder you care about is:

```text
Ventara Generator/Output/GitHub Update/
```

**Everything in that folder is uploaded as a direct asset of the current GitHub Release.** Do not upload the `Windows`, `macOS`, or `Linux` output folders themselves to the repository.

## Latest release only

Only the current Ventara release needs to remain published here. For example:

```text
Installed Ventara: 1.0.0
GitHub latest:      1.0.1
Result:             Ventara offers 1.0.1
```

Later, when 1.0.2 is ready:

```text
Installed Ventara: 1.0.0 or 1.0.1
GitHub latest:      1.0.2
Result:             Ventara offers 1.0.2
```

You do not need to keep 1.0.0 or 1.0.1 published for this comparison to work.

When replacing the current release:

1. Build the new version on the required platforms.
2. Make sure `Ventara Generator/Output/GitHub Update` contains all of the final update files.
3. On GitHub, open **Releases** and create a new release such as `v1.0.2`.
4. Drag all files from `Ventara Generator/Output/GitHub Update` into the release's **Assets** area.
5. Publish the new release.
6. Verify that it is visible and the required `latest*.yml` files are present.
7. Once the new release is working, delete the older release/tag if you only want the latest version visible.

Publish the new release **before** deleting the old one so Ventara never temporarily sees an empty update feed.

## What should never be uploaded here

Do not upload the Ventara development project or private build material, including:

```text
desktop/
renderer/
main/
test/
node_modules/
Ventara Generator/
legacy/
*.pfx
*.p12
*.pem
*.key
.env
```

Signing certificates, passwords, Apple credentials, and other secrets should also never be placed in this repository or attached to a release.

## In one sentence

**The repository contains only these small information files; the current GitHub Release contains the compiled Ventara applications and updater files.**
