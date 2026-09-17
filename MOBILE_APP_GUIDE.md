# MOBILE_APP_GUIDE.md — Phone apps (Android / iPhone)

Use **Flutter**. It builds one app that works on both Android and iPhone from a single codebase, and it's beginner-friendly.

## What to install (walk them through this first)

1. **Flutter SDK** — https://docs.flutter.dev/get-started/install
   - Tell them to download it and follow the installer for their OS.
2. **Android Studio** — needed for the Android emulator (a virtual phone on the computer) and Android build tools. Free download.
3. **VS Code** (recommended editor) with the "Flutter" extension installed from the Extensions panel.
4. Confirm it worked by running:

   ```sh
   flutter doctor
   ```

   Explain: this checks everything is installed correctly. Fix any red ❌ items it lists, one at a time, before moving on.

(iPhone builds require a Mac with Xcode — if they're on Windows, tell them plainly: they can build and test the Android version fully, but building for iPhone needs a Mac, or a cloud Mac service like Codemagic later.)

## Creating the project

```sh
flutter create my_app
cd my_app
```

Explain: this creates a new folder with a working, empty app template.

## Running it

```sh
flutter run
```

Explain: this launches the app on a connected phone or the emulator. First run is slow; that's normal.

## Where the code goes

- `lib/main.dart` — the starting point of the app. Nearly all their code changes will happen inside `lib/`.
- Keep each screen in its own file inside `lib/screens/`.
- Keep reusable pieces (buttons, cards) inside `lib/widgets/`.

## Common beginner tasks — quick reference

| They want to... | Do this |
| --- | --- |
| Add a new screen | Create a new `.dart` file in `lib/screens/`, define a `StatelessWidget` or `StatefulWidget` class |
| Save data on the phone | Use the `shared_preferences` package for simple data, or `sqflite` for a local database |
| Call an online database | Use Supabase (see `DEPLOYMENT_GUIDE.md`) with the `supabase_flutter` package |
| Add an icon/image | Put it in an `assets/` folder, register it in `pubspec.yaml` |
| Add a new package/library | Run `flutter pub add <package_name>` |

## Building the installable app file

- **Android (.apk, installable file):**

  ```sh
  flutter build apk --release
  ```

  The file appears at `build/app/outputs/flutter-apk/app-release.apk`. This can be sent directly to an Android phone and installed (they may need to allow "install from unknown sources").
- **Google Play Store (.aab):**

  ```sh
  flutter build appbundle --release
  ```

  Explain this is only needed if they want to publish on the Play Store, which requires a one-off $25 developer account.
- **iPhone:** requires a Mac + Xcode + a $99/year Apple Developer account to publish to the App Store. Flag this clearly as the one part that costs money and needs Apple hardware.

## When stuck

Most Flutter errors are shown clearly in the terminal under "Exception" or "Error:". Read the first red line back to the user in plain English before suggesting a fix.
