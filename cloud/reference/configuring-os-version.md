# Configuring OS Version

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

### Android

You can configure your Flows to run on a specific Android OS version (API level) using the `android-api-level` parameter when running the `maestro cloud` command:

```
maestro cloud --android-api-level 30 myapp.apk myflows/
```

If you're using one of the CI integrations, please refer to the CI documentation for your specific integration:

{% content-ref url="../ci-integration/" %}
[ci-integration](../ci-integration/)
{% endcontent-ref %}

#### Emulator specs

* x86\_64 architecture
* Android API 33 (Google APIs) **(Default)**
* 606x1280, 244 dpi\\

**Supported API levels:**

| Android Version             | API Level                  |
| --------------------------- | -------------------------- |
| Android 14 Upside Down Cake | 34 (Google APIs)           |
| Android 13 Tiramisu         | 33 (Google APIs) (default) |
| Android 12 Snow Cone        | 31 (Google APIs)           |
| Android 11 Red Velvet Cake  | 30 (Google APIs)           |
| Android 10 Quince Tart      | 29 (Google APIs)           |

### iOS

Flows will be run on iOS simulators

#### Simulator Specs

* ARM or x86 architecture (via Rosetta)
* iOS version 16 (default)
* iPhone 11 (default)
* 828x1792, 326 ppi (iPhone 11)

### Using the `ios-version` parameter (deprecated)

You can configure your Flows to run on a specific iOS major version using the `ios-version` parameter when running the `maestro cloud` command:

```
maestro cloud --ios-version 17 myapp.app myflows/
```

Maestro will automatically select an appropriate minor version, meaning that if you specify iOS 16 your Flows will for example be run on 16.2. If you happen to specify a minimum deployment target version that is below the selected minor version (for example 16.0), an error message will be surfaced with instructions on how to recover.

Notice this mode is deprecated and will be removed in a future release. Current supported values are `16`, `17` and `18`. If you use this flag, your tests will always run with an iPhone 11 simulator.

### Using a specific iOS minor version & device (recommended)

You can configure your Flows to run on a specific iOS runtime and device using the `--device-os` and `--device-model` flags when running the `maestro cloud` command.

The following values are supported:

* \--device-model - `iPhone-11`, `iPhone-13-mini`, `iPhone-16-Pro`, `iPhone-16`, `iPhone-16-Pro`, `iPhone-16-Pro-Max`, `iPad-10th-generation`
* \--device-os - `iOS-16-2`, `iOS-17-5`, `iOS-18-2`

Please note that not all runtimes are available for all devices. This table covers the available combinations:

| Device Model         | iOS Version                  |
| -------------------- | ---------------------------- |
| iPhone-11            | iOS-16-2, iOS-17-5, iOS-18-2 |
| iPhone-13-mini       | iOS-18-2                     |
| iPhone-16-Pro        | iOS-18-2                     |
| iPhone-16-Pro-Max    | iOS-18-2                     |
| iPhone-16            | iOS-18-2                     |
| iPad-10th-generation | iOS-16-2, iOS-17-5, iOS-18-2 |

For example, to run your Flows on iOS 18.2 with an iPhone 16 Pro, you would use:

```
maestro cloud --device-os iOS-18-2 --device-model iPhone-16-Pro myapp.app myflows/
```
