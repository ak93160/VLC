# VLC Android — Original Theme + Next/Previous Navigation

This repository stores the custom navigation patch and a reproducible GitHub Actions build workflow.

## Included changes

- Keep VLC's original theme system and original appearance unchanged.
- Keep the in-player Previous and Next controls visible.
- Use the current VLC playlist when it has adjacent items.
- When a single local `file://` video was opened from a file manager and the playlist has no adjacent item, build a naturally sorted queue from indexed videos in the same folder.

SAF `content://`, network streams, and videos not indexed by VLC's media library continue to use the playlist supplied by VLC or the launching app.

## Build an APK

1. Open the **Actions** tab in this repository.
2. Choose **Build VLC Android APK**.
3. Press **Run workflow**.
4. Download the `VLC-Android-OriginalTheme-NextPrev-Debug-APK` artifact from the successful run.

A push to `main` that changes the patch or workflow also starts a build.

## Source and reproducibility

The workflow checks out the official `videolan/vlc-android` source at commit `14a7422459ca809b29cad567c3a59702178cb423` (the exact upstream snapshot corresponding to the supplied master ZIP), applies `patches/vlc-next-prev.patch`, and builds the debug APK. The official source is not copied or forked into this repository; only this project's small custom patch and build workflow are stored here.

The workflow uses the official source's published LibVLC and medialibrary dependencies for the Debug build; it does not compile the native VLC engine from source.
