# VLC Android — Stable 3.7.1 + Original Theme + Next/Previous Navigation

This repository builds the customization against the official **stable VLC Android 3.7.1** source tag, not a Nightly or beta snapshot.

## Included changes

- Keep VLC's original theme system and original appearance unchanged.
- Keep the in-player Previous and Next controls visible.
- Use the current VLC playlist when it has adjacent items.
- When a single local `file://` video was opened from a file manager and the playlist has no adjacent item, build a naturally sorted queue from indexed videos in the same folder.

SAF `content://`, network streams, and videos not indexed by VLC's media library continue to use the playlist supplied by VLC or the launching app.

## Build an APK

1. Open the **Actions** tab in this repository.
2. Choose **Build VLC Android Stable 3.7.1 APK**.
3. Press **Run workflow**.
4. Download the `VLC-Android-3.7.1-Stable-OriginalTheme-NextPrev-Universal-Debug-APK` artifact from the successful run.

A push to `main` that changes the patch or workflow also starts a build.

## Source and reproducibility

The workflow fetches the official `videolan/vlc-android` Git tag `3.7.1`, applies `patches/vlc-next-prev.patch`, and builds the debug APK. The tag is used rather than a moving Nightly/master revision. The official upstream source is fetched during the build; this repository stores only this project's custom patch and build workflow.

The workflow uses the official source's published LibVLC and medialibrary dependencies for the Debug build; it does not compile the native VLC engine from source. The resulting APK is a universal APK containing ARM64, ARMv7, x86, and x86_64 native libraries.
