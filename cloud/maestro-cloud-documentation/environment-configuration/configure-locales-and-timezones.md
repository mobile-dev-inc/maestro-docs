---
description: >-
  Configure specific app locales and understand default device timezones in
  Maestro Cloud.
---

# Configure locales and timezones

Maestro Cloud allows you to configure specific app locales and understand the default timezone settings for its cloud environments. This is essential for testing internationalization (i18n) and features that depend on localized data or time.

{% hint style="info" %}
**Maestro Cloud Plan required.** Locale and timezone configuration features are available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Configure app locale

Use the `--device-locale` parameter with the `maestro cloud` command to automatically change the device locale for an upload.

The parameter value must follow the format `[`[`ISO-639-1`](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) `language code]_[`[`ISO-3166-1`](https://en.wikipedia.org/wiki/ISO_3166-1) `country code]`. Below you find two examples:

```bash
# Set device locale to German (Germany)
maestro cloud --device-locale de_DE <APP_FILE> <WORKSPACE>

# Set device locale to Japanese (Japan)
maestro cloud --device-locale ja_JP <APP_FILE> <WORKSPACE>
```

If the parameter is omitted, the default locale is `en_US`.

{% hint style="info" %}
#### Locales supported by Maestro&#xD;

Check the [documentation](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/test-in-different-locales/locales-supported-by-maestro) to find the complete list of supported locales.
{% endhint %}

### Default device timezones

Maestro Cloud instances are located in specific regions with default timezones, listed in the following table:

| Device type | Physical location (Region)                                                         | Default Timezone |
| ----------- | ---------------------------------------------------------------------------------- | ---------------- |
| **Android** | `us-west1-a` ([Google Cloud](https://cloud.google.com/compute/docs/regions-zones)) | UTC              |
| **iOS**     | `vegas`                                                                            | GMT -7           |

The Region refers to the physical location of the test environment. This environment can be either:

* an emulated setup (a Linux instance running an Android emulator), or
* a simulated setup (a macOS instance running an iOS simulator).

A device can override some region-level settings. For example, the Android emulator uses the UTC timezone by default, regardless of the region.
