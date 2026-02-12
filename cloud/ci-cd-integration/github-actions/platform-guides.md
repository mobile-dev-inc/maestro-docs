---
description: Set up Maestro Cloud GitHub Actions for Android, iOS, and Flutter.
---

# Platform guides

This guide covers platform-specific configurations for setting up Maestro Cloud GitHub Actions.

{% tabs %}
{% tab title="Android" %}
To run tests on Android, you generally need to build an ARM compatible APK (typically a debug build) and upload it to Maestro Cloud.

#### Build command

Use Gradle to assemble your debug APK before the Maestro step.

```yaml
- uses: actions/setup-java@v3
  with:
    java-version: 11
    distribution: 'temurin'

- run: ./gradlew assembleDebug
```

#### Action configuration

Point the `app-file` to your generated APK.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v2.0.1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: app/build/outputs/apk/debug/app-debug.apk
```

{% hint style="info" %}
The `app-file` path supports glob patterns. If multiple files match, the first one is used.
{% endhint %}

#### ProGuard deobfuscation

If your app uses ProGuard/R8, you should upload the mapping file to deobfuscate performance traces and error logs.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v2.0.1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: app/build/outputs/apk/release/app-release.apk
    mapping-file: app/build/outputs/mapping/release/mapping.txt
```

#### Specifying Android API level

The default API level on Maestro Cloud is 33 (Android 13). You can override this using `android-api-level`.

```yaml
with:
  # ... other inputs
  android-api-level: 29
```

#### Complete example for Android

The following code snippet shows a complete GitHub Action to build your Android app and test is using Maestro Cloud.

```yaml
name: Build and run Maestro tests (Native Android)

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  maestro-cloud:
    runs-on: ubuntu-latest
    outputs:
      app: app/build/outputs/apk/debug
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: 11
          distribution: 'temurin'
      - run: ./gradlew assembleDebug
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: app/build/outputs/apk/debug/app-debug.apk
```
{% endtab %}

{% tab title="iOS" %}
To run tests on iOS, you must build your app for the iOS Simulator. Real device builds (ARM64 only) are not supported on the Cloud emulators.

#### Build command

You must specify `-destination 'generic/platform=iOS Simulator'` to ensure the build is compatible with Maestro Cloud simulators.

```yaml
- name: Build for Simulator
  run: |
    xcodebuild build \
      -scheme 'MyApp' \
      -configuration Debug \
      -project 'MyApp.xcodeproj' \
      -destination 'generic/platform=iOS Simulator' \
      CONFIGURATION_BUILD_DIR=$PWD/build
```

#### Action configuration

Point the `app-file` to the `.app` bundle generated in your build directory.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: build/MyApp.app
```

#### Uploading symbol files (.dSYM)

To get symbolicated stack traces, include the generated `.dSYM` file.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: build/MyApp.app
    mapping-file: build/MyApp.app.dSYM
```

#### Specify the iOS Version and device

The default iOS version is 16. You can specify a different OS version or device model if needed, using `device-os` and  `device-model`  respectively:&#x20;

```yaml
with:
  # ... other inputs
  device-model: iPhone-16
  device-os: iOS-18-2
```

#### Complete example for iOS

The following code snippet shows a complete GitHub Action to build your iOS app and test is using Maestro Cloud.

```yaml
name: Build and run Maestro tests (Native iOS)

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: macOS-latest
    steps:
      - uses: actions/checkout@v2
      - run: xcodebuild build -scheme 'MyApp' -configuration Debug -project 'MyApp.xcodeproj' -destination 'generic/platform=iOS Simulator' CONFIGURATION_BUILD_DIR=$PWD/build
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: build/MyApp.app
```
{% endtab %}

{% tab title="Untitled" %}


### Flutter

Flutter requires specific build flags to generate binaries compatible with Maestro Cloud.

#### Flutter Android

Build the APK in debug mode.

```yaml
name: Build and run Maestro tests (Flutter Android)

on:
  workflow_dispatch:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          channel: "stable"
      - run: flutter build apk --debug
      - uses: mobile-dev-inc/action-maestro-cloud@v2.0.1
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: build/app/outputs/flutter-apk/app-debug.apk
```

#### Flutter iOS

Build the iOS app for the simulator.

```yaml
name: Build and run Maestro tests (Flutter iOS)

on:
  workflow_dispatch:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ios:
    runs-on: macos-13
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          channel: "stable"
      - run: flutter build ios --debug --simulator
      - uses: mobile-dev-inc/action-maestro-cloud@v2.0.1
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: build/ios/iphonesimulator/Runner.app # replace `Runner` with your app name
```
{% endtab %}
{% endtabs %}

#### Next Steps

* [Advanced configuration](advanced-configuration.md): Learn how to configure async mode, environment variables, and custom workspaces.
* [Outputs and triggers](outputs-and-triggers.md): Learn how to use action outputs and configure CI triggers.
