# Pixel Snake: Play Store project

An Android project (Capacitor) that wraps the Snake game. The game itself lives in `www/index.html` and works fully offline.

- App name: Pixel Snake
- Package name: `com.janakpurwebstudio.pixelsnake` (permanent once uploaded; change it first in `capacitor.config.json`, `android/app/build.gradle` and `android/app/src/main/res/values/strings.xml` if you want another)
- Target SDK 36, portrait only, no permissions

## What you need once
1. A Google Play Developer account (one-time USD 25 fee, identity check).
2. A signing key. Make it once and keep it safe, a lost key cannot be replaced:

   keytool -genkeypair -v -keystore release.keystore -alias pixelsnake -keyalg RSA -keysize 2048 -validity 10000

   Back up `release.keystore` and its passwords somewhere private. Never commit it.

## Build the .aab (easiest: GitHub, no Android Studio)
1. Put this folder in a new private GitHub repository.
2. Repository Settings > Secrets and variables > Actions > add four secrets:
   - `KEYSTORE_BASE64`: output of `base64 -w0 release.keystore` (on Mac: `base64 -i release.keystore`)
   - `KEYSTORE_PASSWORD`, `KEY_ALIAS` (pixelsnake), `KEY_PASSWORD`
3. Actions tab > "Build Play Store bundle" > Run workflow.
4. Download `pixel-snake-release-aab` from the finished run. That `app-release.aab` is the file Play wants.

Each run raises the version code automatically, so you can upload updates.

## Build locally instead (Android Studio)
    npm install
    npx cap sync android
Open the `android` folder in Android Studio, then Build > Generate Signed App Bundle.

## Publish
1. Host `PRIVACY_POLICY.md` as a web page (GitHub Pages or a page on your own site). Play requires a public URL.
2. Play Console > Create app > Pixel Snake, Game, Free.
3. Store listing: copy text from `store/LISTING.md`, upload the icon, feature graphic and screenshots from `store/`.
4. App content: privacy policy URL, ads = No, data safety = no data collected, content rating questionnaire (see LISTING.md).
5. Testing: upload the .aab to a testing track first. New personal developer accounts must run a closed test with a minimum number of testers for a minimum number of days before production access. The numbers have changed before, so read the current rule in Play Console.
6. Production > Create release > upload .aab > Send for review. Review usually takes a few days.

## Change the game
Edit `www/index.html`, then run `npx cap sync android` and build again.
