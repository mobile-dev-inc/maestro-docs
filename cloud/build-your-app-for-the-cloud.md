# Build your app for the cloud

Before you can execute tests on Maestro Cloud, you must provide a mobile application binary (APK or `.app` directory). This page provides the specific technical requirements and build instructions for the most common development environments to ensure your app is compatible with Maestro's cloud infrastructure.

#### General binary requirements

Regardless of your framework, your application must meet these core specifications for cloud compatibility:

* **Architecture**:&#x20;
  * Android builds must be compatible with x86\_64 architecture.
  * iOS builds must be compatible with x86 or ARM (via Rosetta).
* **File Formats**:
  * Android: APK files are required; AAB (Android App Bundle) is currently not supported.
  * iOS: You must provide a path to an `*.app` simulator build directory or a zipped file containing that directory.
* **Build Types**: Both Release and Debug builds are supported for both iOS and Android.

#### Android build instructions

{% tabs %}
{% tab title="Build with Gradle" %}
Run the following commands from your project root to generate the APK. Once finished, find the file in the `app/build/outputs/apk/` directory.

```bash
# To generate a Debug build
./gradlew assembleDebug

# To generate a Release build
./gradlew assembleRelease
```
{% endtab %}

{% tab title="Build with Flutter" %}
Use the Flutter CLI to create a compatible APK. The result will be located in the `build/app/outputs/flutter-apk/` folder. You can use anyone of the following commads:

```bash
# Debug build (Recommended for initial testing)
flutter build apk --debug

# Release build
flutter build apk
```
{% endtab %}
{% endtabs %}

#### iOS Build Instructions

{% tabs %}
{% tab title="Build with Xcode CLI" %}
Use the `xcodebuild` command to create a simulator build. The following example builds a project named `MyApp` and saves the output to a `build/` folder:

```bash
xcodebuild -project MyApp.xcodeproj \
  -scheme MyApp \
  -configuration Debug \
  -destination 'generic/platform=iOS Simulator' \
  CONFIGURATION_BUILD_DIR=$PWD/build
```

The `.app` bundle will be available in the `build/` directory.
{% endtab %}

{% tab title="Build with Fastlane" %}
If you use [Fastlane](https://fastlane.tools/) for automation, the script should look the following one to generate the app file:

```ruby
xcodebuild(
    configuration: build_config[:configuration],
    scheme: build_config[:scheme],
    workspace: build_config[:xcode_workspace],
    xcargs: "-quiet -sdk 'iphonesimulator' -destination 'generic/platform=iOS Simulator'",
    derivedDataPath: IOS_DERIVED_DATA_PATH # this will contain the .app which we need later on
)
```
{% endtab %}

{% tab title="Building with Flutter" %}
Use the following command to create a simulator-compatible debug build:

```bash
flutter build ios --debug --simulator
```

The app bundle is located in the `build/ios/iphonesimulator/` directory.
{% endtab %}
{% endtabs %}

#### Next Steps: Running the Build

Once your binary is ready, you can upload it to Maestro Cloud using the CLI or Maestro Studio:

* Maestro CLI: Use the command `maestro cloud [your-app-binary] [your-flow-directory]`.
* Maestro Studio: Click "Run on Cloud" in the sidebar and select your newly built binary.

#### Related Documentation

* [Cloud Quickstart](https://www.google.com/search?q=quickstart): Run your first test using sample apps.
* [GitHub Actions](https://www.google.com/search?q=github-actions): Automate these build steps directly in your CI pipeline.
* [CLI Reference](https://www.google.com/search?q=cloud-cli-reference): Explore advanced flags for your cloud uploads.

Next Step: Would you like me to draft the [GitHub Actions](https://www.google.com/search?q=github-actions) page next to show you how to automate these build commands in your repository?
