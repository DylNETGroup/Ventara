# Publish a Ventara update

GitHub is used only as Ventara's public update/download endpoint. Do not paste the Ventara source tree into this repository.

## For each version

1. Build and test the production release locally on Windows, macOS, and Linux.
2. On GitHub, open **Releases → Draft a new release**.
3. Use the exact Ventara version as the tag, for example `v1.0.1`.
4. Attach every file from your local:

   `Releases/1.0.1/GitHub Upload/`

5. Keep every generated filename unchanged.
6. Publish only after the intended platform packages and updater manifests are present.

## Important updater assets

The release should contain the generated platform packages together with **all** generated `latest*.yml` files and `.blockmap` files. These must be direct GitHub Release assets; do not put them inside another ZIP.

The repository itself can stay as small as this README and the release instructions. The release assets are stored by GitHub Releases, not as committed repository folders.
