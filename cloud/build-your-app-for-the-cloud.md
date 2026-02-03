# Build your app for the cloud

Before you can execute tests on Maestro Cloud, you must provide a mobile application binary (APK or `.app` directory). This page provides the specific technical requirements and build instructions for the most common development environments to ensure your app is compatible with Maestro's cloud infrastructure.

{% hint style="success" %}
This feature requires a Cloud plan. Start for free at [**maestro.dev**](https://signin.maestro.dev/sign-up).
{% endhint %}

### Android build instructions

Maestro Cloud uses x86\_64 and x86 architectures for Android. Ensure your app binary meets the following requirements:

* **Format:** APK only. Android App Bundles (.aab) are not currently supported.
* **Architecture:** Must be compatible with x86\_64 or x86. ARM-only APKs will fail to launch in the cloud environment.
* **Build Type:** Both Release and Debug builds are supported.

To build your app, use one of the following approaches:&#x20;

{% tabs %}
{% tab title="Build with Gradle" %}
Run the following commands from your project root to generate the APK.&#x20;

```bash
# To generate a Debug build
./gradlew assembleDebug

# To generate a Release build
./gradlew assembleRelease
```

Once finished, find the file in the `app/build/outputs/apk/` directory.
{% endtab %}

{% tab title="Build with Flutter" %}
Use the Flutter CLI to create a compatible APK. You can use anyone of the following commands:

```bash
# Debug build (Recommended for initial testing)
flutter build apk --debug

# Release build
flutter build apk
```

The result will be located in the `build/app/outputs/flutter-apk/` folder.&#x20;
{% endtab %}
{% endtabs %}

### iOS build instructions

Maestro Cloud runs iOS tests on Simulators. Do not upload binaries built for physical iOS devices.

* **Format:** `.app` bundle.
* **Target:** Must be built for the iOS Simulator.

To build your app, use one of the following options:&#x20;

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

### Run the build

Once your binary is ready, you can upload it to Maestro Cloud using the Maestro CLI or Maestro Studio:

{% tabs %}
{% tab title="Maestro CLI" %}
Use the command:

```bash
maestro cloud [your-app-binary] [your-flow-directory]
```
{% endtab %}

{% tab title="Maestro Studio" %}
You can choose to run all or a single Flow on Maestro Cloud:

* **Run all Flows:** Click on the **Run on Cloud** button in the sidebar and then select your app binary.
* **Run a single Flow**: Open the Flow file,click on the **Run on Cloud** button on at the top of the file, and then select your app binary.
{% endtab %}
{% endtabs %}

#### Next steps

Now that you know how to build you app, you can explore one of the following categories of guides to improve your process of using Maestro Cloud:

* [ci-cd-integration](ci-cd-integration/ "mention")
* [environment-configuration](environment-configuration/ "mention")
* [notifications](notifications/ "mention")
* [advanced-features](advanced-features/ "mention")

If you didn't test Maestro CLI yet, check the [how-to-run-your-tests-on-maestro-cloud.md](how-to-run-your-tests-on-maestro-cloud.md "mention") guide.
