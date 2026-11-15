# VLC Android — Stable 3.7.1 + Original Theme + Next/Previous + Gemini AI Subtitles

This project modifies the official **VLC Android 3.7.1 stable** source tag. It does not use Nightly or a moving master branch.

## Included features

- Original VLC theme and appearance retained, with the stable orange/red launcher icon.
- In-player Previous and Next controls. When VLC receives a one-item local file playlist, the app can build a naturally sorted queue from indexed videos in the same folder.
- AI Translate entry in the subtitle controls.
- External subtitle import: SRT, WebVTT, ASS and SSA.
- Best-effort extraction of embedded text subtitle tracks when Android's MediaExtractor exposes them as readable text samples.
- Google Gemini batch translation with Hindi as the default target language; target language and Gemini model can be selected.
- Pause and Resume with a persistent per-batch checkpoint, retry/backoff, saved progress, elapsed time, ETA, completed/remaining cue counts and batch status.
- Encrypted at-rest API-key storage using Android Keystore, local translated-subtitle cache, translated SRT export, and loading the translated subtitle back into VLC.
- Optional original + translated subtitle display.

## Gemini setup

1. Open a video and open its subtitle controls.
2. Select **AI Translate**.
3. Add your own Gemini API key, choose an embedded text track or an external subtitle file, then choose the target language.
4. Start translation. Pause at any time; Resume continues from the last saved batch.
5. Choose **Use translated subtitle in VLC** or export the translated SRT file.

Subtitle text and nearby context are sent to Google's Gemini API for translation. The API key is encrypted locally with Android Keystore, but a key used inside a mobile app can still be exposed on rooted or compromised devices. Use your own key and configure usage limits in your Google AI project. The app does not bundle or publish a shared key.

## Subtitle limitations

Embedded subtitle extraction depends on the Android demuxer/codec exposing readable timed text samples. It is best-effort, not universal for every container or subtitle codec. Image-based tracks such as PGS and VobSub are not OCR-converted; use an external text subtitle instead. Some embedded formats do not expose exact cue-end timestamps, so an end time may need to be estimated. External subtitle timestamps are preserved from the source file.

## Build

Open the **Actions** tab and run **Build VLC Android Stable 3.7.1 with Gemini AI Subtitles**, or push a change to `patches/**`, `patch-parts/**`, the workflow, or this README on `main`.

The workflow fetches the official VideoLAN `3.7.1` stable tag, applies the checked-in customization patch, creates a full patched source ZIP, then builds one universal signed Release APK for ARM64, ARMv7, x86 and x86_64. The native VLC engine is supplied by the published LibVLC dependency for this Android Release build.

The CI APK is signed with a temporary CI key, not VideoLAN's Play Store signing key. It cannot update an official VLC install with a different signing certificate; uninstall that app before installing this build.
