# Ventara

Ventara is a desktop web browser built with Electron and Chromium, with a custom interface, tab management, private browsing, bookmarks, history, downloads, themes, backgrounds, profiles, extensions, and built-in update support.

The Electron version is cross-platform and does not require Microsoft Edge WebView2.

## Platforms

Ventara can be built for:

- Windows x64
- macOS
- Linux x64

Builds are distributed as portable/unpacked applications rather than traditional installers.

## Getting started

### Requirements

- Node.js 22.12 or newer
- npm
- Git

Clone the repository, then install the dependencies:

```bash
cd desktop
npm ci
```

Run Ventara in development mode:

```bash
npm start
```

Run the checks and tests:

```bash
npm run build
npm test
```

## Building Ventara

You can build directly from the `desktop` folder:

```bash
npm run dist:win
npm run dist:mac
npm run dist:linux
```

Build each platform on its native operating system.

There is also a **Ventara Generator** folder containing simple build launchers for Windows, macOS, and Linux.

### Release builds

The update builds intended for GitHub are generated into:

```text
Ventara Generator/
└── Output/
    ├── release.json
    ├── Windows/
    ├── Mac/
    └── Linux/
```

Set the release number once in `Ventara Generator/Version`, then run the single build script for the platform you are building:

```text
Ventara Generator/Windows/Build-Windows.bat
Ventara Generator/macOS/Build-macOS.command
Ventara Generator/Linux/Build-Linux.sh
```

Each script creates an unpacked copy of Ventara and places it in the matching folder under `Ventara Generator/Output`.

## Updates

Ventara uses a whole-folder updater.

The public repository contains a `Releases` directory with the current builds:

```text
Releases/
├── release.json
├── Windows/
├── Mac/
└── Linux/
```

Ventara checks `release.json`, selects the build for the current operating system, downloads and verifies the files, then stages the update.

When the user chooses **Restart & install**, Ventara closes and replaces the existing application files with the new build in the same installation location.

On macOS, the complete `Ventara.app` bundle is replaced.

User settings and browser data are stored separately from the application files and are not removed during an update.

There are no version-number folders in the update repository. Locally, `Ventara Generator/Version` is the version you edit. The generator copies that version into Ventara itself and into `release.json`.

## Updating Chromium

Ventara uses the Chromium version bundled with Electron. Chromium is therefore updated by updating Electron rather than replacing Chromium separately.

To update the Electron runtime:

```bash
cd desktop
npm run engine:update
```

After updating, test the browser, change `Ventara Generator/Version`, rebuild each platform, and upload the new contents of `Ventara Generator/Output` to the repository's `Releases` folder.

## Project layout

```text
desktop/
├── main/        Electron main process and browser/update logic
├── renderer/    Ventara interface
├── scripts/     Build and release tools
├── test/        Automated tests
├── assets/      Icons, backgrounds and other bundled assets
└── package.json

Ventara Generator/
├── Windows/
├── macOS/
├── Linux/
└── Output/

legacy/
└── WinForms/    Original Windows version retained for reference
```

## Main features

- Tabs, pinned tabs and tab groups
- Private tabs and private windows
- Bookmarks and browsing history
- Download manager
- Search engine and homepage settings
- Light, dark and custom interface themes
- Custom backgrounds and classic Ventara backgrounds
- Profile pictures and display names
- Find in page, zoom, printing and developer tools
- Extension loading and management
- Session restore
- Legacy Ventara data import
- Automatic and manual update checking

## Development notes

The Electron application is located in `desktop`. The original WinForms version is kept under `legacy/WinForms` and is not part of the Electron build.

The production browser uses the update files stored under `Releases` in the GitHub repository. Development builds do not install online updates unless they are built using the update generator scripts.

For more detail about creating releases, see [BUILD-AND-RELEASE.md](BUILD-AND-RELEASE.md).
