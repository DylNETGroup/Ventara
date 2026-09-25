# Ventara

Ventara is a desktop web browser built with Electron and Chromium, with a custom interface, tab management, private browsing, bookmarks, history, downloads, themes, backgrounds, profiles, extensions, and built-in updates.

The Electron version is cross-platform and does not require Microsoft Edge WebView2.

## Platforms

Ventara can be built for:

- Windows x64
- macOS
- Linux x64

Windows builds include both an unpacked portable build and a normal installer. The portable build is also used by Ventara's automatic updater.

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

## Ventara Generator

Normal releases are made from the `Ventara Generator` folder.

```text
Ventara Generator/
├── Version
├── Build-Windows.bat
├── Build-macOS.command
├── Build-Linux.sh
└── Output/
    ├── release.json
    ├── Windows/
    │   ├── Portable/
    │   └── Installer/
    ├── Mac/
    └── Linux/
```

Set the release number once in `Ventara Generator/Version`, for example:

```text
1.2.0
```

Then run the build command for the operating system you are building on. The generator applies that version to Ventara automatically before compiling.

### Windows

Run:

```text
Ventara Generator/Build-Windows.bat
```

This creates both:

- `Output/Windows/Portable` — the complete unpacked application used for automatic updates.
- `Output/Windows/Installer` — a normal Windows installer for new/manual installations.

The installer is named `Ventara-Setup-<version>.exe`.

### macOS and Linux

Run `Build-macOS.command` on macOS or `Build-Linux.sh` on Linux. Their update builds are placed directly in `Output/Mac` and `Output/Linux`.

Each generator refreshes only the output it owns. Building Windows does not delete the Mac or Linux builds.

## Publishing updates

Ventara's public update files use this layout in the repository:

```text
Releases/
├── release.json
├── Windows/
├── Mac/
└── Linux/
```

For Windows, copy the **contents** of:

```text
Ventara Generator/Output/Windows/Portable/
```

into:

```text
Releases/Windows/
```

Do not copy the `Portable` wrapper folder itself. Also copy `Ventara Generator/Output/release.json` to `Releases/release.json`.

For macOS and Linux, copy `Output/Mac` to `Releases/Mac` and `Output/Linux` to `Releases/Linux`.

The Windows installer is not used by the automatic updater. It can be attached to the GitHub Release for people installing Ventara for the first time.

## Updates

Ventara uses a whole-folder updater. It checks `Releases/release.json`, compares the published version with the version built into the app, and selects the files for the current operating system.

When an update is downloaded, every file is verified before installation. After the user chooses to restart and install, Ventara closes and replaces the application files in the existing installation location with the new portable build.

On macOS, the complete `Ventara.app` bundle is replaced. User settings and browser data are stored separately from the application files and are not removed during an update.

There are no version-number folders in the update repository and no separate public `Version` file is required. `Ventara Generator/Version` is the version you edit locally; the generator writes the same version into Ventara and `release.json`.

## Updating Chromium

Ventara uses the Chromium version bundled with Electron, so Chromium is updated by updating Electron.

```bash
cd desktop
npm run engine:update
```

After updating Electron, test Ventara, change `Ventara Generator/Version`, rebuild each platform, and publish the new update files.

## Project layout

```text
desktop/
├── main/        Electron main process and browser/update logic
├── renderer/    Ventara interface
├── scripts/     Build and release tools
├── test/        Automated tests
├── assets/      Icons, backgrounds and bundled assets
└── package.json

Ventara Generator/
├── Version
├── Build-Windows.bat
├── Build-macOS.command
├── Build-Linux.sh
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

Production builds made through the generator have the stable update channel enabled. Development builds do not install online updates.

For more detail about creating releases, see [BUILD-AND-RELEASE.md](BUILD-AND-RELEASE.md).
