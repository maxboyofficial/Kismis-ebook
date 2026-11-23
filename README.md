# Kismis eBook Reader

Kismis is a lightweight Android e-book reader built with Kotlin and Jetpack Compose. It pairs a translucent frosted-glass navigation dock with fast offline reading, live Project Gutenberg catalog browsing, custom library organization, and built-in read-aloud playback.

## Features

- **White & Dark Themes**: Switch between a bright white paper theme with crisp dark outlines and a low-glare dark mode, with a dark frosted-glass floating dock (and side navigation rail on tablets) plus a draggable white pill indicator with haptic feedback.
- **1,000+ Classics & Gutendex Catalog**: Includes 8 bundled offline books across major genres, auto-warms ~100 titles on launch, supports infinite scroll, and provides a one-tap **Load 1,000+** sync to index over 1,000 public domain titles locally.
- **Dynamic Library Organization**: Browse downloaded books by All Books, Bookmarks, Genre, Author, or custom `#tags` that you can create and assign per book. Also supports importing local `.txt` files via Android's file picker.
- **Customizable Reader**: Choose between horizontal page swiping or continuous vertical scrolling, adjust font size, line spacing, typeface (Serif, Sans, Display), and paper surface (Auto, White, Sepia, Dark), with balanced line widths on tablets.
- **Enhanced Text-to-Speech (TTS)**: Gapless sentence pre-buffering, natural text cleanup, voice presets (`Storyteller`, `Natural`, `Calm Night`, `Crisp Fast`), pitch/speed sliders, voice preview, sleep timer, and automatic audio-focus pausing.
- **Low-RAM & Tablet Optimized**: Automatic hardware RAM detection with a configurable **Lite Mode** (reduced overdraw, zero-shadow surfaces, RGB565 cover thumbnails, and lightweight Room catalog projections) plus adaptive multi-column grids on tablets and foldables.

## Tech Stack

- **Language & UI**: Kotlin, Jetpack Compose, Material 3
- **Persistence**: Room (books, bookmarks, custom tags, reading progress) & DataStore Preferences (theme and typography settings)
- **Networking**: Retrofit, OkHttp, Moshi (`https://gutendex.com/books`)
- **Images & Audio**: Coil, Android `TextToSpeech`

## Building Locally

Requires JDK 17, Android SDK (API 36), and Gradle 9.3.1.

1. Decode the included debug keystore so debug builds sign cleanly:
   ```bash
   base64 -d debug.keystore.base64 > debug.keystore
   ```
2. Run unit and Robolectric tests:
   ```bash
   gradle testDebugUnitTest
   ```
3. Build the debug APK:
   ```bash
   gradle assembleDebug
   ```
   The APK will be generated at `app/build/outputs/apk/debug/app-debug.apk`.

## Automated GitHub Releases

Pushing to `main` or `master` (or pushing a `v*` tag) triggers `.github/workflows/build.yml`, which runs tests, compiles `Kismis-debug.apk`, uploads build artifacts, and publishes the APK directly to the repository's **Releases** page.

To also publish a signed release APK (`Kismis-release.apk`), add the following repository secrets in GitHub Settings:

- `RELEASE_KEYSTORE_BASE64`: Base64-encoded `.jks` upload keystore (alias `upload`)
- `STORE_PASSWORD`: Keystore password
- `KEY_PASSWORD`: Key password
