---
description: >-
  Configure app locales and understand default device timezones in Maestro Cloud
  to test internationalization and time-dependent features.
---

# App locales and device timezones

Maestro Cloud allows you to configure specific app locales and understand the default timezone settings for its cloud environments. This is essential for testing internationalization (i18n) and features that depend on localized data or time.

{% hint style="info" %}
**Maestro Cloud Plan required.**&#x20;

Locale configuration features are available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Configure app locale

Use the `--device-locale` parameter with the `maestro cloud` command to automatically change the device locale for an upload.

The parameter value must follow the format `[`[`ISO-639-1`](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) `language code]_[`[`ISO-3166-1`](https://en.wikipedia.org/wiki/ISO_3166-1) `country code]`. Below you find two examples:

```bash
# Set device locale to German (Germany)
maestro cloud --device-locale de_DE --app-file <APP_FILE> --flows <WORKSPACE>

# Set device locale to Japanese (Japan)
maestro cloud --device-locale ja_JP --app-file <APP_FILE> --flows <WORKSPACE>
```

If the parameter is omitted, the default locale is `en_US`.

{% hint style="info" %}
#### Locales supported by Maestro&#xD;

Check the [documentation](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/test-in-different-locales/locales-supported-by-maestro) to find the complete list of supported locales.
{% endhint %}

### Default device timezones

All Maestro Cloud instances are physically located in Las Vegas, USA. While the physical location is the same for all devices, the default timezones differ between platforms:

| Platform    | Default Timezone | Offset |
| ----------- | ---------------- | ------ |
| **Android** | UTC              | +00:00 |
| **iOS**     | Pacific Time     | GMT -7 |

It is important to note that these timezones are fixed and cannot currently be configured via CLI flags or configuration files. If your tests depend on specific time-of-day logic, ensure your assertions account for these offsets.

* **Android:** Regardless of the physical host region, the Android emulator defaults to UTC.
* **iOS:** iOS simulators inherit the system time of the host macOS instance, which is set to GMT -7.

### Related content

Now that you understand how locales and timezones work in the Maestro Cloud, explore other ways to customize your test environment:

* [configure-the-os.md](configure-the-os.md "mention"): Run your tests on specific Android API levels or iOS versions.
* Set up notifications via [Slack](../notifications/set-slack-notification.md), [email](../notifications/set-email-notification.md), or [webhooks](../notifications/configure-webhooks.md) to stay informed about build and test results.
