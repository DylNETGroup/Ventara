# Ventara

Official Ventara download and update endpoint.

This public repository intentionally contains **no Ventara application source code**. The newest compiled Ventara version is published on the **Releases** page and is also used by Ventara's built-in updater.

## Latest release only

Only the current Ventara release needs to remain published here. When replacing it:

1. publish the new version first (for example `v1.0.1`);
2. upload all files produced in `Ventara Generator/Output/GitHub Update` as direct release assets;
3. verify the new release is live;
4. then delete the older release/tag if you do not want release history.

Ventara compares the installed version with the newest published release metadata. Old releases are not needed for that comparison.
