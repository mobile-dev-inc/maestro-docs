# Test in different locales

Testing how your app handles different languages and regional formats is critical for a global user base. In Maestro, the locale is a global device setting. Because changing the system language requires a device-level configuration change, it is handled via the CLI only at runtime.&#x20;

{% hint style="info" %}
There is no place in a Flow (such as `launchApp` or `config.yaml`) to define the locale. The locale must be provided at execution time using the CLI or a CI wrapper (for example, GitHub Actions).
{% endhint %}

{% hint style="info" %}
#### Web support

Maestro can change the locale for Android and iOS devices, but it does not control the internal language settings of the Chrome browser used for Web tests.
{% endhint %}

#### Set the locale

To run a Flow in a specific language, use the `--device-locale` flag when executing commands from the terminal. The value passed to `--device-locale` must be a combination of an [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) language code and an [ISO-3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) country code, separated by an underscore (`_`).

You can use `--device-locale` with the `maestro start-device` and `maestro cloud` commands. It is not possible to define the locale when running the `maestro test` command.

Refer to [locales-supported-by-maestro.md](locales-supported-by-maestro.md "mention") for the full list of supported locales.

The following examples show how to start devices with specific locales.

{% tabs %}
{% tab title="Android" %}
```bash
# Create a new Android emulator with the locale set to France (French)
maestro start-device \
  --platform android \
  --device-locale fr_FR
```
{% endtab %}

{% tab title="iOS" %}
```bash
# Create a new iOS simulator with the locale set to Italy (Italian)
maestro start-device \
  --platform ios \
  --device-locale it_IT
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### What happens to the device?

When you start a device and define a locale, Maestro attempts to change the system language and region of the connected simulator or emulator before running any Flow.
{% endhint %}

After starting the device with the desired locale, you can run your tests normally. Maestro continues using the locale defined during device initialization.

```bash
maestro test your_flow.yaml
```

#### Combine locales and tags

If certain tests should only run in specific languages (for example, tests that validate French translations), a recommended approach is to combine `--device-locale` with [tags](../../workspace-management/test-discovery-and-tags.md). This ensures that only tests relevant to the selected locale are executed, making test runs faster and more efficient.

First, define a tag in the Flow. In the following example, the `french` tag indicates that the Flow is intended to validate the app using the French translation.

```yaml
# flows/login_fr.yaml
appId: com.example.app
tags:
  - french
---
- launchApp
- assertVisible: "Bienvenue"
```

After tagging your Flows, specify the tag when running tests using the `--include-tags` flag.

```bash
# Start the Android device using the French locale
maestro start-device --platform android --device-locale fr_FR
# Run only tests tagged as French
maestro test --include-tags french .maestro/
```

#### Related Documentation

* [locales-supported-by-maestro.md](locales-supported-by-maestro.md "mention"): Check the full list of supported locales.
* [Maestro CLI overview](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/ "mention"): Learn how to execute flows using the CLI.
* [test-discovery-and-tags.md](../../workspace-management/test-discovery-and-tags.md "mention"): Learn how to group and filter your localization tests.
