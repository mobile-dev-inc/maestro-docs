---
description: >-
  Specify Android API levels or iOS runtime versions and device models for your
  cloud tests.
---

# Configure the OS

Maestro Cloud allows you to test your application across multiple Android and iOS versions. This ensures your app remains compatible and performs reliably across different mobile environments.

{% hint style="info" %}
**Maestro Cloud Plan required.** OS configuration options are available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Android

You can specify the Android OS version (API level) using the `--android-api-level` flag when using Maestro Cloud.

```bash
maestro cloud --android-api-level <API_LEVEL> <APP_FILE> <FLOWS>
```

The following table lists the supported Android versions:

| Android Version | API Level | Notes                     |
| --------------- | --------- | ------------------------- |
| Android 14      | 34        | Google APIs               |
| **Android 13**  | **33**    | **Default (Google APIs)** |
| Android 12      | 31        | Google APIs               |
| Android 11      | 30        | Google APIs               |
| Android 10      | 29        | Google APIs               |

### iOS

For iOS, you can configure both the runtime version and the device model.

Maestro recommends specifying both the minor OS version and the device model. Use the `--device-os` and `--device-model` flags to select a specific combination:

```bash
maestro cloud --device-os <DEVICE_OS> --device-model <DEVICE_MODEL> <APP_FILE> <FLOWS>
```

The following table lists the supported device models and their available iOS versions:

| Device Model             | Supported iOS Versions       |
| ------------------------ | ---------------------------- |
| **iPhone-11**            | iOS-16-2, iOS-17-5, iOS-18-2 |
| **iPhone-13-mini**       | iOS-18-2                     |
| **iPhone-16**            | iOS-18-2                     |
| **iPhone-16-Pro**        | iOS-18-2                     |
| **iPhone-16-Pro-Max**    | iOS-18-2                     |
| **iPad-10th-generation** | iOS-16-2, iOS-17-5, iOS-18-2 |

For example, to run your flows on iOS 18.2 using an iPhone 16 Pro, use the following command:

```bash
maestro cloud --device-os iOS-18-2 --device-model iPhone-16-Pro myapp.app myflows/
```

{% hint style="info" %}
#### Deprecated: `--ios-version` &#x20;

The `--ios-version` option is deprecated and will no longer be available. Use the `--device-os` and `--device-model` flags instead.



Previously, the `--ios-version` flag allowed you to specify only a major version (for example, `16`, `17`, or `18`). When using this flag, Maestro Cloud automatically runs your flows on an **iPhone 11** simulator.
{% endhint %}
