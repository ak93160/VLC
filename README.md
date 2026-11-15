# VLC Android — Stable 3.7.1 + Original Theme + Next/Previous + Gemini AI Subtitles

This project builds against the official **VLC Android 3.7.1 stable** tag. It does not use Nightly or a moving master branch.

## Included features

- Original VLC theme, appearance, and stable orange/red launcher icon.
- In-player Previous and Next navigation. When VLC receives a one-item local file playlist, it can build a naturally sorted queue from indexed videos in the same folder.
- **Gemini AI Subtitle Translation** from the subtitle-track options menu.
- Hindi as the default translation language, editable target language and Gemini model.
- External subtitle input: SRT, WebVTT, ASS, SSA.
- Best-effort embedded text subtitle extraction through Android `MediaExtractor` for tracks the platform/container exposes as readable text samples.
- Timestamp-preserving translated SRT output, optional original + translated lines, and SRT export.
- Background WorkManager processing with Pause, Resume, retry, encrypted API-key storage, per-batch checkpoints, progress, elapsed time, ETA and status reporting.

## Gemini setup

1. Open a video in VLC and open the subtitle-track options.
2. Choose **AI Translate**.
3. Enter your own Gemini API key, select an external subtitle file or extract a supported embedded text track, and choose the target language.
4. Start translation. Progress is saved after each successful batch; use Resume after pausing or an interruption.
5. Select **Use translated subtitle in VLC** or export the translated SRT file.

Subtitle text is sent to Google's Gemini API. The key is encrypted at rest with Android Keystore, but a key used directly by a mobile app can still be exposed on a rooted or compromised device. Use your own key and set usage limits in your Google AI project.

## Subtitle limitations

Embedded extraction is best-effort and depends on Android's supported text extractors and the video's container/codec. Image-based tracks such as PGS and VobSub are not OCR-converted. For those tracks, select an external text subtitle file. If an embedded format does not expose an exact cue-end time, the extracted cue end is estimated, so exact synchronization cannot be guaranteed for every embedded format. External subtitle timestamps are retained as supplied.

## Build

Open the repository's **Actions** tab and run **Build VLC Android Stable 3.7.1 APK**, or push a change to `patches/**`, the workflow, or `README.md` on `main`. The workflow builds one universal signed Release APK with ARM64, ARMv7, x86, and x86_64 libraries and uploads a full Stable source ZIP.

The CI APK uses a temporary signing key, not VideoLAN's Play Store key. It cannot be installed as an update over the official Play Store VLC app without first uninstalling the app that has the different signature.
