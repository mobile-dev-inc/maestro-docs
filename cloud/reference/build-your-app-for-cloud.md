# Build your app for the cloud

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

## iOS

### Building with Xcode command line tools

To build an app with Xcode command line tools **xcrun xcodebuild** should be used. Here is an example on how to build an app called `MyApp` for iOS simulator target:

```
xcodebuild -project MyApp.xcodeproj \
-scheme MyApp \
-configuration Debug \
-destination 'generic/platform=iOS Simulator' \
CONFIGURATION_BUILD_DIR=$PWD/build
```

The `.app file` will then be located `build/` folder, which can be modified via the last parameter of the script.

### Building with Fastlane

If you use [fastlane](https://fastlane.tools/) for your automation pipelines the script should look the following way:

```
xcodebuild(
      configuration: build_config[:configuration],
      scheme: build_config[:scheme],
      workspace: build_config[:xcode_workspace],
      xcargs: "-quiet -sdk 'iphonesimulator' -destination 'generic/platform=iOS Simulator'",
      derivedDataPath: IOS_DERIVED_DATA_PATH # this will contain the .app which we need later on
)
```

### Building with Flutter

If you use Flutter to build your app you can create a debug build for simulators using the following command:

```
flutter build ios --debug --simulator
```

You can then find your app file in the `build/ios/iphonesimulator/` directory.

## Android

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
