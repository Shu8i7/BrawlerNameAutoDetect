# Brawler Auto Detect (Android source project)

## What changed

This is a replacement project for the manual-input test APK (v3). The app **does not offer manual brawler name entry**. It shows a click-through overlay at the top right of LDPlayer and attempts to read the selected Brawler's name from the actual Brawl Stars character/detail screen via on-device OCR.

Flow: launch the app -> grant **Display over other apps** -> tap Start -> grant Android screen capture -> open the Brawl Stars character detail/selection screen so the character name is visible -> after two consecutive successful recognitions (about 2-5 seconds) it displays the name in the top right -> keeps that name when returning to the match.

### Important limitations (do not skip)

* It can identify a character **only while the name is visible on screen**. A lobby or match screenshot containing only a 3D model, as in the screenshots provided, **does not supply enough information for OCR**. Visual identification from the model requires a separately trained image classifier and real reference screenshots; it is not implemented here.
* This is **source code, not an installable APK**. Android SDK/Gradle/ML Kit binaries are unavailable in this execution environment, so installation and runtime have **not been tested**. Do not rename the zip as APK.
* The app never reads the game process or its account data and never uploads screen images. Screen-capture permission must be confirmed by the user per capture session. Some games/LDPlayer settings may block screen recording, which would also block recognition.
* The character name table has known English/Japanese names and may need updates for new characters or alternate translations. If the selected name is not in the table, it stays in detection-waiting state.
* The overlay only displays a name; does not automate inputs.

### Generate APK online (Android Studio not required)

1. Create a GitHub repository.
2. Upload **the contents of this folder**, including the hidden `.github` folder, so `settings.gradle` is at the repository root.
3. Use **Actions > Build APK > Run workflow**.
4. From the successful build, download the artifact ZIP, unzip and install `app-debug.apk` into LDPlayer.

Because this build cannot be executed here, it may require adjustments for an Android or LDPlayer version; check Actions build logs. If you have the old v3 APK installed, uninstall it so the old manual overlay doesn't remain on screen.

Build specs: Java 17, Gradle 8.9, AGP 8.7.3, compileSdk 35, minSdk 26, targetSdk 34, offline bundled Latin/Japanese ML Kit OCR.
