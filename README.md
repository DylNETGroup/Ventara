# Ventara

Ventara is a native C++ desktop browser for Windows, with a custom glass interface, an interactive bubble-based Home page and built-in customization tools.

[Download the latest release](https://github.com/DylNETGroup/Ventara/releases/latest) · [All releases](https://github.com/DylNETGroup/Ventara/releases)

## Features

- **Glass interface:** custom window controls, menus and appearance settings.
- **Bubble Home page:** shortcuts, folders, a pin bar, and free or snapped placement.
- **Tabs and tab folders:** pinned tabs, grouping, reordering and session restoration.
- **Bookmarks:** folders, folder colours, favicons and a bookmarks bar.
- **Personalization:** animated backgrounds, custom images and interface colours.
- **Browsing tools:** history, downloads, private browsing, privacy settings and extension management.
- **Pop-out video:** a floating mini-player with playback controls.
- **Ventara AdShield:** an optional built-in ad and tracker blocker, disabled by default and available in Experimental.
- **Built-in updates:** checks GitHub Releases for a newer version and installs after confirmation.

Experimental features may change or behave differently across websites. AdShield depends on the browser runtime's extension support; compatibility can change as that runtime evolves.

## Requirements

- Windows 10 or Windows 11, **64-bit x64**. Windows 11 provides the closest intended glass appearance.
- Microsoft Edge WebView2 Runtime installed.
- An internet connection for browsing, downloads and update checks.

The current native release targets Windows. macOS and Linux builds from the discontinued Electron project are not compatible with it.

## Download and run

1. Open the [latest release](https://github.com/DylNETGroup/Ventara/releases/latest).
2. Under **Assets**, download **`Windows-Release.zip`**. The automatically generated **Source code** archives are not the built application.
3. Extract the complete ZIP to a normal folder. Do not run Ventara from inside the ZIP.
4. Open the extracted folder and run **`Ventara.exe`**.

Keep the complete application contents together, including `WebView2Loader.dll`, `Addons`, `Licenses` and `THIRD-PARTY-NOTICES.txt`. The add-on files are needed even when AdShield is disabled.

## Updates

Ventara checks for updates shortly after startup and every six hours while running. You can also open **About → Check for updates**.

When a newer release is available, choose **Install update** and confirm. Ventara downloads and verifies the package, saves the session, closes, replaces the application folder and reopens. Session restoration follows your existing preference. The previous application folder is retained as a sibling recovery backup named with `.ventara-old-...`.

Settings and browsing data are stored separately under:

```text
%LOCALAPPDATA%\Ventara
```

The updater uses the latest published **stable GitHub release**, its numeric version tag and its attached Windows ZIP. It does not use the old repository `Releases/release.json` or `update.json` files. Pre-releases and drafts are not offered by the current updater.

### If an update fails

- **HTTP 404 while checking:** confirm there is a publicly accessible, published stable release. A draft, pre-release or tag without a published release is not sufficient.
- **HTTP 404 while downloading:** the selected asset may have been removed or replaced. Restart Ventara, check again and confirm the release asset can be downloaded.
- **ZIP is incomplete:** the package must contain the complete built application folder, with its loader, `Licenses` folder and notices beside `Ventara.exe`.
- **Size or SHA-256 verification failed:** restart and check again after the release upload has finished. Do not install a partial or mismatched package.
- **Installation or restart failed:** retain the existing installation and recovery backup. Check the `update.log` path shown in the error. Update jobs are stored under `%LOCALAPPDATA%\Ventara\NativeUpdates`.

## Build from source

Use the current native source package containing **`Ventara.sln`**. The release asset contains the built application; it may not contain the source project.

1. Install Visual Studio 2022 with **Desktop development with C++**, the **v143 toolset** and a Windows SDK.
2. Open `Ventara.sln`.
3. Select **Release** and **x64**.
4. Close any running copy of Ventara from that build folder.
5. Choose **Build → Rebuild Solution** and wait for a successful result.
6. Run the new `Ventara.exe` from the output `Release` folder.

The native project uses C++20. Keep the bundled dependencies, resources and project settings with the source.

## Publish a new update

1. Before building, update all three version values in `Ventara/core/Version.h`. For example, a **0.1.0** build uses:

   ```cpp
   #define VENTARA_VERSION "0.1.0"
   #define VENTARA_VERSION_RESOURCE 0, 1, 0, 0
   #define VENTARA_VERSION_RESOURCE_STRING "0.1.0.0\0"
   ```

2. Rebuild **Release/x64** and check the version in About.
3. Manually ZIP the **complete built Release folder** as **`Windows-Release.zip`**. Zipping the folder itself or its contents both work. Include exactly one `Ventara.exe`; do not include old build backups. `Ventara.pdb` is optional debug information and can be excluded.
4. Create a GitHub release with the matching numeric tag, for example **`v0.1.0`**, and attach the ZIP. Upload one unambiguous Windows x64 application ZIP.
5. Leave **Set as a pre-release** unticked, mark the intended release **Latest**, and publish after the upload finishes.
6. Test the update from a separate, older native build.

**The release tag determines the update version, not the ZIP filename or release title.** The published version must be newer than the installed version: `0.1.0` updates `0.0.9`, but does not update `1.0.0`. Keep the ZIP filename the same across releases if desired. No separate update manifest is required.

## Third-party components

Ventara includes third-party components with their own licence terms. Ventara AdShield is powered by the bundled uBlock Origin filtering engine. Attribution and licence information are included in `THIRD-PARTY-NOTICES.txt`, the `Licenses` folder and the bundled component files. Keep these notices with redistributed builds.
