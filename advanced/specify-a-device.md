---
description: >-
  Select specific devices for testing with --device, list simulators or
  emulators and use sharding to run flows in parallel.
---

# Specify a Device

If you have multiple devices open, you can specify which device to run Maestro on. To do this, you must first obtain the device identifier and then pass it to Maestro.

### Obtain the device identifier

{% tabs %}
{% tab title="Android" %}
To list available Android devices, run the following command in your terminal:

```bash
adb devices
```

From the output, locate the device identifier for the device you want to use with Maestro.
{% endtab %}

{% tab title="iOS" %}
To list available iOS simulators, run the following command in your terminal:

```bash
xcrun simctl list devices booted
```

From the output, locate the device identifier for the device you want to use with Maestro.
{% endtab %}
{% endtabs %}

## Pass the device identifier to Maestro

When running any Maestro command that requires a device (e.g. `test` or `studio`), you must first pass the device identifier with the `--device` parameter before running the command.

For example, to run Maestro Studio on an Android device with identifier `emulator-5554` use the following command:

```css
maestro --device emulator-5554 studio
```

Similarly, to run `flow.yaml` on an iOS simulator with identifier `5B6D77EF-2AE9-47D0-9A62-70A1ABBC5FA2` use the following command:

```
maestro --device 5B6D77EF-2AE9-47D0-9A62-70A1ABBC5FA2 test flow.yaml
```

## Run flows in parallel

Maestro can run tests in parallel, also known as "sharding".

{% embed url="https://youtu.be/VS1TqvZz398" %}

There are two sharding strategies available.

### --shard-all

To run tests in parallel, you can use the `--shard-all` parameter. This parameter will run the same tests in parallel on available devices:

```
maestro test --shard-all 3 .maestro
```

### --shard-split

Let’s say you have 3 running devices and 9 tests, but now you want to split this test suite into 3 chunks of tests and run them in parallel on connected devices:

```
maestro test --shard-split 3 .maestro
```

{% hint style="warning" %}
To run with `--shard-all 3` or `--shard-split`, you need to have 3 available devices. If there are less, Maestro will print an error and request you to run more devices.
{% endhint %}
