# Magnet to TorBox (Android)

A tiny Android app that registers itself as a handler for `magnet:` links. Tap a magnet link in
any browser or app and it is sent to your [TorBox](https://torbox.app) account through
`POST /v1/api/torrents/createtorrent`. A small dialog shows "Sending…" and then the result, and
closes itself on success. No third-party libraries: only the Android framework.

## Build the APK

You need a debug APK, signed automatically with the debug key. That is fine for installing
on your own phone.

- **Android Studio:** open this folder, let Gradle sync, then *Build → Build APK(s)*.
- **Command line** (JDK 17+ and the Android SDK installed):
  `./gradlew assembleDebug`, which produces `app/build/outputs/apk/debug/app-debug.apk`.
- **GitHub, no local setup:** push this folder to a new GitHub repo. The workflow in
  `.github/workflows/build-apk.yml` runs on every push (or from the *Actions* tab →
  *Build APK* → *Run workflow*); download `magnet-to-torbox-apk` from the finished run.

Then copy the APK to the phone, open it, and allow "install unknown apps" for your file
manager or browser when Android asks.

## Set up

1. Open **Magnet to TorBox**, paste your TorBox API key (torbox.app → Settings), tap
   **Test key**, then **Save**.
2. Tap a magnet link anywhere. If Android asks which app to open it with, choose
   **Magnet to TorBox** and tap **Always**. If you have another torrent app installed it may
   ask each time until you do this.

The app also has a box for pasting a magnet link by hand.

## Notes

- Requires Android 8.0 (API 26) or newer.
- The API key is kept in the app's private storage, excluded from backups, and sent only
  to `https://api.torbox.app`.
- TorBox limits uncached torrents to 60 per hour per API token. Errors from TorBox
  (active limit, plan limit, bad key and so on) are shown in the dialog as TorBox words them.
- Seeding can be set in the app. "Use my TorBox account setting" leaves the field out.
- The package name is `com.example.magnettotorbox`. Change `namespace` and `applicationId` in
  `app/build.gradle.kts` (and the Kotlin `package` lines) if you want your own.
- Versions: Android Gradle Plugin 8.7.3, Kotlin 2.0.21, Gradle 8.10.2, compile/target SDK 35.
