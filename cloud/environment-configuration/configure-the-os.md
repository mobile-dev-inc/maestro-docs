---
description: >-
  Set OS versions and device models for Maestro Cloud tests using the
  `--device-os` and `--device-model` flags. Supports Android 10-14 and iOS
  16-26.
---

# Configure the OS

Maestro Cloud allows you to test your application across multiple Android and iOS versions. This ensures your app remains compatible and performs reliably across different mobile environments.

{% hint style="info" %}
**Maestro Cloud Plan required.** OS configuration options are available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Full list of supported Cloud devices

You can access the full list of supported Cloud devices and operating systems by using the following command:

```bash
maestro list-cloud-devices
```

### Android

For Android, you can configure both the OS version and the device model. Use the `--device-os` and `--device-model` flags to select a specific combination:

```bash
maestro cloud --device-os "<DEVICE_OS>" --device-model "<DEVICE_MODEL>" --app-file "<APP_FILE>" --flows "<FLOWS>"
```

The following table lists the supported Android versions:

| Android Version          | Device OS / API Level |
| ------------------------ | --------------------- |
| Android 14               | android-34            |
| **Android 13 (Default)** | **android-33**        |
| Android 12               | android-31            |
| Android 11               | android-30            |
| Android 10               | android-29            |

For example, to run your flows on Android 14 using a Pixel 6, use the following command:

```bash
maestro cloud --device-os "android-34" --device-model "pixel_6" --app-file myapp.apk --flows myflows/
```

Run `maestro list-cloud-devices` to see the full list of supported Android device models.

{% hint style="info" %}
#### Reproducing Cloud runs locally

To closely reproduce Maestro Cloud runs for Android on your local machine, create an emulator of the same API version and use the Google APIs variant (not Google Play).
{% endhint %}

### iOS

For iOS, you can configure both the runtime version and the device model.

Maestro recommends specifying both the minor OS version and the device model. Use the `--device-os` and `--device-model` flags to select a specific combination:

```bash
maestro cloud --device-os "<DEVICE_OS>" --device-model "<DEVICE_MODEL>" --app-file "<APP_FILE>" --flows "<FLOWS>"
```

The following table lists an example of the supported device models and their available iOS versions:

| Device Model             | Supported iOS Versions                 |
| ------------------------ | -------------------------------------- |
| **iPhone-11**            | iOS-16-4, iOS-17-5, iOS-18-2, iOS-26-2 |
| **iPhone-13-mini**       | iOS-18-2, iOS-26-2                     |
| **iPhone-16**            | iOS-18-2, iOS-26-2                     |
| **iPhone-17-Pro**        | iOS-26-2                               |
| **iPhone-17-Pro-Max**    | iOS-26-2                               |
| **iPad-10th-generation** | iOS-16-4, iOS-17-5, iOS-18-2, iOS-26-2 |

For example, to run your flows on iOS 26.2 using an iPhone 17 Pro, use the following command:

```bash
maestro cloud --device-os "iOS-26-2" --device-model "iPhone-17-Pro" --app-file myapp.app --flows myflows/
```

Run `maestro list-cloud-devices` to see the full list of supported iOS device models and OS versions.

{% hint style="info" %}
#### Deprecated: `--ios-version`  & `--android-api-level`

The `--ios-version` and `--android-api-level` options are deprecated and will be removed in a future release. Use the `--device-os` and `--device-model` flags instead.



Previously, the `--ios-version` flag allowed you to specify only a major version (for example, `16`, `17`, or `18`). When using this flag, Maestro Cloud automatically runs your flows on an **iPhone 11** simulator.
{% endhint %}

### Related content

Now that you understand how configure the OS, explore other ways to customize your test environment:

* [app-locales-and-device-timezones.md](app-locales-and-device-timezones.md "mention"): Select the device locale for Maestro Cloud tests.
* Set up notifications via [Slack](../notifications/set-slack-notification.md), [email](../notifications/set-email-notification.md), or [webhooks](../notifications/configure-webhooks.md) to stay informed about build and test results.
