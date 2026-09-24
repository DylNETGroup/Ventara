# Ventara — Simple Update Publishing Guide

This GitHub repository is only used to host **Ventara downloads and updates**.

The Ventara source code stays on the development computer and is **not uploaded here**.

## What goes in this GitHub repository?

Only this README needs to be stored in the normal repository files.

```text
Ventara/
└── README.md
```

The compiled Ventara applications are uploaded through **GitHub Releases**, not added to the repository folders.

---

# Publishing a new Ventara update

## 1. Change the Ventara version

Before building a new release, update the Ventara version in the local project.

For example:

```text
1.0.0 → 1.0.1
```

The new version must be higher than the version users already have installed.

## 2. Build the update versions

Open the local:

```text
Ventara Generator
```

Use the **Update** builder for each operating system being released.

### Windows

Run:

```text
Windows/Build-Windows-Update.bat
```

### macOS

Run:

```text
macOS/Build-macOS-Update.command
```

### Linux

Run:

```text
Linux/Build-Linux-Update.sh
```

Each builder places its finished files into:

```text
Ventara Generator/Output/
```

The files intended for GitHub are automatically collected in:

```text
Ventara Generator/Output/GitHub Upload/
```

## 3. Check the GitHub Upload folder

After all required platforms have been built, the folder should contain files similar to:

```text
GitHub Upload/
├── Ventara-1.0.1-win-x64.exe
├── Ventara-1.0.1-win-x64.exe.blockmap
├── latest.yml
│
├── Ventara-1.0.1-mac-universal.dmg
├── Ventara-1.0.1-mac-universal.zip
├── Ventara-1.0.1-mac-universal.zip.blockmap
├── latest-mac.yml
│
├── Ventara-1.0.1-linux-x64.AppImage
├── Ventara-1.0.1-linux-arm64.AppImage
└── latest-linux*.yml
```

The exact filenames may vary slightly depending on the build.

**Only upload the files inside `GitHub Upload`.**

Do not upload the Ventara source project, `node_modules`, unpacked builds, certificates, or development files.

## 4. Open the GitHub release page

On Windows, the easiest option is to run:

```text
Ventara Generator/Open-GitHub-Publish.bat
```

This opens the GitHub release page and the `GitHub Upload` folder.

Otherwise, open the Ventara repository on GitHub and go to:

```text
Releases → Draft a new release
```

## 5. Create the release

For Ventara 1.0.1, use:

```text
Tag:   v1.0.1
Title: Ventara 1.0.1
```

The tag version must match the version that was compiled.

## 6. Drag the files into GitHub

Open:

```text
Ventara Generator/Output/GitHub Upload/
```

Select everything inside the folder and drag it into the **Attach binaries by dropping them here** area on the GitHub release page.

Wait for every file to finish uploading.

## 7. Publish the release

Click:

```text
Publish release
```

The new release is now the version Ventara checks for updates.

---

# What happens after publishing?

Ventara checks the latest published GitHub Release.

For example:

```text
Installed version: 1.0.0
Latest GitHub version: 1.0.1
```

Ventara sees that `1.0.1` is newer and can download the correct update for the user's operating system.

The generated files such as:

```text
latest.yml
latest-mac.yml
latest-linux.yml
```

contain the version and update information Ventara needs. A separate `currentVersion.json` file is not required.

---

# Keeping only the latest release

It is fine to keep only the newest Ventara release on GitHub.

When replacing 1.0.1 with 1.0.2:

1. Build and upload **1.0.2**.
2. Publish **1.0.2** first.
3. Confirm the new release works.
4. Delete the old **1.0.1** release if it is no longer needed.

Always publish the new release before deleting the old one so Ventara never has a period with no available update feed.

---

# Quick version

For every new Ventara update:

```text
1. Increase Ventara version
2. Run the Windows/macOS/Linux Update builders
3. Open Ventara Generator/Output/GitHub Upload
4. Create a new GitHub Release
5. Use tag v<version>
6. Drag everything from GitHub Upload into the release
7. Click Publish release
8. Test updating from the previous Ventara version
9. Delete the old GitHub Release if desired
```

That is the complete publishing process.
