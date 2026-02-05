---
description: >-
  Download sample Flows and app with maestro download-samples, then install and
  run them on iOS or Android using maestro test.
---

# Run a Sample Flow

{% hint style="info" %}
If you want to get started writing your own Flow right away, skip ahead to the [**next section**](writing-your-first-flow.md).
{% endhint %}

### Download the Samples

Use the download-samples command to download the samples:

```shell
maestro download-samples
```

This will download the build-in sample Flows and app into a `samples/` folder in your current directory.

### Run the Sample Flow

Install the sample app and then run the associated Flow using the `maestro test` command.

{% tabs %}
{% tab title="iOS" %}
```shell
cd ./samples
unzip sample.zip
xcrun simctl install Booted Wikipedia.app
maestro test ios-flow.yaml
```
{% endtab %}

{% tab title="Android" %}
```
cd ./samples
adb install sample.apk
maestro test android-flow.yaml
```
{% endtab %}
{% endtabs %}
