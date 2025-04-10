# Configuring OS Version

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
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
* 606x1280, 244 dpi\


**Supported API levels:**

| Android Version             | API Level                  |
| --------------------------- | -------------------------- |
| Android 14 Upside Down Cake | 34 (Google APIs)           |
| Android 13 Tiramisu         | 33 (Google APIs) (default) |
| Android 12 Snow Cone        | 31 (Google APIs)           |
| Android 11 Red Velvet Cake  | 30 (Google APIs)           |
| Android 10 Quince Tart      | 29 (Google APIs)           |

### iOS

Flows will be run on iOS simulators&#x20;

#### Simulator Specs

* x86 architecture
* iOS version 16 (default)
* iPhone 11
* 828x1792, 326 ppi

**Supported iOS runtimes:**

* iOS 16 (default)
* iOS 17
* iOS 18

You can configure your Flows to run on a specific iOS major version using the `ios-version` parameter when running the `maestro cloud` command:

```
maestro cloud --ios-version 17 myapp.app myflows/
```

Maestro will automatically select an appropriate minor version, meaning that if you specify iOS 16 your Flows will for example be run on 16.2. If you happen to specify a minimum deployment target version that is below the selected minor version (for example 16.0), an error message will be surfaced with instructions on how to recover.\

#### Using a specific iOS minor version & device

You can also configure your Flows to run on a specific iOS minor version and device using the `--device-os` and `--device-model` parameters when running the `maestro cloud` command. The following values are supported:

* --device-model - `iPhone-11`, `iPad-10th-generation`, `Apple-TV-4K-3rd-generation-4K`, `Apple-Watch-Series-10-46mm`
* --device-os - `iOS-16-2`, `iOS-16-4`, `iOS-17-5`, `iOS-18-2`, `watchOS-11-2`, `tvOS-18-2`
