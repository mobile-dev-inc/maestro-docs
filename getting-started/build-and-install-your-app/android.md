# Android

Android app binary requirements:

* APK (AAB not supported)
* Compatible with x86\_64 architecture
* Release and Debug builds both supported

## Building with Gradle

Build your app using one of the commands below. Then find the appropriate APK file in the `build/outputs/apk/` output directory.

```sh
# Release build
./gradlew assembleRelease

# Debug build
./gradlew assembleDebug
```

## Building with Flutter

If you use Flutter to build your app you can create a debug build using the following command:

```bash
# Release build
flutter build apk

# Debug build
flutter build apk --debug
```

You can then find the built apk in the `build/app/outputs/`folder.
