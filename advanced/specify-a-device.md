# Specify a Device

If you have multiple devices open, you can specify which device to run Maestro on. To do this, you must first obtain the device identifier and then pass it to Maestro.

{% hint style="info" %}
Note that when you specify a device, Maestro will not start the device.
{% endhint %}

### Obtaining the Device Identifier

{% tabs %}
{% tab title="Android" %}
To list your running Android devices, run the following command in your terminal:

```bash
adb devices
```

From the output, locate the device identifier for the device you want to use with Maestro.
{% endtab %}

{% tab title="iOS" %}
To list your running iOS simulators, run the following command in your terminal:

```bash
xcrun simctl list devices booted
```

From the output, locate the device identifier for the device you want to use with Maestro.
{% endtab %}
{% endtabs %}

### Passing the Device Identifier to Maestro

When running any Maestro command that requires a device (e.g. `test` or `studio`), you must first pass the device identifier with the `--device` parameter before running the command.

For example, to run Maestro Studio on an Android device with identifier `emulator-5554` use the following command:

```css
maestro --device emulator-5554 studio
```

Similarly, to run Maestro Test on an iOS simulator with identifier `5B6D77EF-2AE9-47D0-9A62-70A1ABBC5FA2` use the following command:

```
maestro --device 5B6D77EF-2AE9-47D0-9A62-70A1ABBC5FA2 test flow.yaml
```

{% hint style="warning" %}
Even with multiple devices open, Maestro is unable to run tests in parallel.
{% endhint %}
