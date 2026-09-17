# Mobile apps — Flutter

Follow [Start here](START_HERE.md) first. Flutter is the default for a new app that needs Android and iOS from a shared codebase. Keep an existing stack when appropriate.

## Inspect and install only what is needed

Check the host OS, Flutter SDK, available devices, and platform build tools. Use the official installation guide for that operating system. Android work needs the Android SDK and a physical device or emulator; Android Studio can manage those tools. An editor is optional if the assistant can edit files directly.

```sh
flutter doctor
flutter devices
```

Resolve issues relevant to the target platform. Do not block an Android-only task on missing tools for unrelated platforms. Some platform licenses or device approvals may need the user's action; explain the exact step.

iOS builds require macOS and Xcode, locally or on an authorized hosted build machine. Explain this early if the current computer cannot build the chosen target. Local development and App Store distribution have different account requirements; check current Apple documentation before requesting paid enrollment.

## Create and run

Use a new folder and a valid project name:

```sh
flutter create my_app
cd my_app
flutter run
```

Select a known available device if more than one is connected. Use `lib/main.dart` as the starting point, group screens and reusable widgets sensibly, and avoid excessive architecture for a small first version.

Use preference storage for small non-sensitive settings and a suitable local database for structured records. Use platform-backed secure storage for credentials where needed. Add a backend only for requirements such as shared data, accounts, or synchronization.

Treat client-side configuration as discoverable. Public Supabase keys can be used with properly configured access policies; secret/service-role keys must stay on a trusted backend. See [web app security guidance](WEB_APP_GUIDE.md#protect-data-at-the-backend).

## Verify behavior

```sh
flutter analyze
flutter test
```

Replace template-only tests with meaningful checks for the actual app. Exercise the main journey on a target device or emulator, including restart persistence, keyboard behavior, small screens, and relevant network or permission failures. Test offline behavior if it is promised.

If the app has accounts, test that users cannot access one another's private records. State explicitly when testing was limited to an emulator or one platform.

## Build for the intended distribution route

For Android:

```sh
flutter build apk --release
flutter build appbundle --release
```

Choose the APK for direct device testing or distribution when appropriate, and the app bundle for a Play Store release. Configure and verify release signing before store submission; a successful release build alone does not establish that store signing is ready. Protect signing keys and passwords, and keep them out of Git.

The normal APK output is `build/app/outputs/flutter-apk/app-release.apk`; use the actual build output to locate artifacts because build options can change filenames.

For iOS, follow Flutter's iOS release guide for identifiers, signing, provisioning, and archive creation on macOS. Use TestFlight or an appropriate authorized distribution route. Do not promise that an iOS build can simply be sent to any phone as an installable file.

Store submission may require paid accounts, identity verification, testing, privacy disclosures, screenshots, and review. Check current requirements and fees rather than hard-coding prices. Ask the user only for decisions or actions that genuinely need them.

Follow [deployment](DEPLOYMENT_GUIDE.md) and verify the actual release artifact.

## Official references

- [Flutter installation](https://docs.flutter.dev/get-started/install)
- [Android release and signing](https://docs.flutter.dev/deployment/android)
- [iOS release and signing](https://docs.flutter.dev/deployment/ios)
