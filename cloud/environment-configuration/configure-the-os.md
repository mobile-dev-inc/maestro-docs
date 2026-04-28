---
description: >-
  Set OS versions and device models for Maestro Cloud tests using the
  `--device-os` and `--device-model` flags.
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

You can specify the Android OS version using the `--device-os` flag when using Maestro Cloud:

```bash
maestro cloud --device-os "<DEVICE_OS>" --app-file "<APP_FILE>" --flows "<FLOWS>"
```

For example, to run your flows on Android 14:

```bash
maestro cloud --device-os "android-34" --app-file myapp.apk --flows myflows/
```

Run `maestro list-cloud-devices` to see the full list of supported Android OS versions.

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
