---
description: >-
  Build and install your Android app for Maestro. Generate APKs with Gradle or
  Flutter, ensure API 26+, and install on an emulator or device.
---

# Android

This assumes you've got the Android SDK bits already installed.&#x20;

If you haven't, and especially if you happen to be using a Mac, this video will take you all the way from zero, through the prequisites, to a running Emulator.

{% embed url="https://www.youtube.com/watch?v=0WhZ4HtepFI" %}

Maestro works with most apps, but there are a few requirements:

* APK (AAB not supported)
* Compatible with x86\_64 architecture
* Requires Android API level 26 or newer
* Release and Debug builds both supported (although Release builds are often better)

## Building with Gradle

Build your app using one of the commands below. Then find the appropriate APK file in the `build/outputs/apk/` output directory.

```sh
# Release build
./gradlew assembleRelease

# Debug build
./gradlew assembleDebug
```

## Building with Flutter

If you use Flutter to build your app you can create a build using the following command:

```bash
# Release build
flutter build apk

# Debug build
flutter build apk --debug
```

You can then find the built apk in the `build/app/outputs/`folder.



## Building with Other Frameworks

We're not going to attempt to cover all the possible ways you could build an app. React Native and Expo both have their standard ways (and, like Gradle, can be customised by the developers to follow any pattern that suits the team). Some rather refined developers might even provide a makefile.



## Running on an Emulator

If you've not already got an emulator running, start one now. You can do that with the Android SDK tools, through the Android Studio, or via Maestro's [Start Device](../../cli/start-device.md) command.

Once that's done, you can you either drag-n-drop the APK onto the running emulator, or run

```
adb install /path/to/app.apk
```

