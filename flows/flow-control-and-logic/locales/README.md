# Locales

Testing how your app handles different languages and regional formats is critical for a global user base. In Maestro, the locale is a global device setting. Because changing the system language requires a device-level configuration change, it is handled via the CLI only at runtime.&#x20;

{% hint style="info" %}
There is no place in the Flow (like `launchApp` or `config.yaml`) to define the locale. It must be passed during execution via the CLI or CI wrapper (like GitHub Actions)
{% endhint %}

{% hint style="info" %}
#### Web support

Maestro can change the locale for Android and iOS, but it has no control over the internal language settings of the Chrome browser (Web tests).
{% endhint %}

#### Set the locale

To run a Flow in a specific language, use the `--device-locale` flag when executing your test from the terminal. When using `--device-locale`, you have to inform a combination of [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) + [ISO-3166-1](https://en.wikipedia.org/wiki/ISO_3166-1), separated by an underscore `_` symbol in between them, to define the desired locale.

You can use the `--device-locale` when running the  `maestro start-device`  or `maestro cloud`. It's not possible to define the locale when running the `test` command.

Access the [locales-supported-by-maestro.md](locales-supported-by-maestro.md "mention") to see all available options.

The following examples show how to start devices with specific locales.

{% tabs %}
{% tab title="Android" %}
```bash
# Create a new Android emulator with locale set to France (French)
maestro start-device \
  --platform android \
  --device-locale fr_FR
```
{% endtab %}

{% tab title="iOS" %}
```bash
# Create a new iOS simulator with locale set to Italy (Italian)
maestro start-device \
  --platform ios \
  --device-locale it_IT
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### What happens to the device?

When you start the define and define the locale, Maestro attempts to change the system language and region of the connected simulator or emulator before running any Flow.
{% endhint %}

After starting the device using the desired locale, you can run your tests normally, while Maestro keeps using the locale you defined in the device initialization.&#x20;

```bash
maestro test your_flow.yaml
```

#### Combine locales and tags

If you have specific tests that should only run in certain languages (e.g., a test that specifically validates French translations), the best practice is to combine `--device-locale` with Tags. This way you ensure only tests related to the desired locale will run, making the testing process faster and more eficient.&#x20;

First, you have to define the tag when creating the Flow. In the following example, the `french` tag is used to identify that the Flow ains to evaluate the app when using the French translation.

```yaml
# flows/login_fr.yaml
appId: com.example.app
tags:
  - french
---
- launchApp
- assertVisible: "Bienvenue"
```

After defining the tags in all your Flows, you need to specify it when running your tests using the CLI by using the `--include-tags` flag.&#x20;

```bash
## Start the Android device using the french locale
maestro start-device --platform android --device-locale fr_FR
# Target only French tests and set the device to French
maestro test --include-tags french .maestro/
```

{% hint style="info" %}
It is not possible to use the `--device-locale` flag when running the `test` command with the CLI.
{% endhint %}

#### Related Documentation

* [Maestro CLI overview](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/ "mention"): Learn how to execute flows using the CLI.
* [test-discovery-and-tags.md](../../workspace-management/test-discovery-and-tags.md "mention"): Learn how to group and filter your localization tests.
