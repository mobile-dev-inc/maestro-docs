# setAirplaneMode

The `setAirplaneMode` command enables or disables airplane mode on the device.&#x20;

{% hint style="info" %}
This command is only available on Android.

iOS simulators don't have an airplane mode.
{% endhint %}

### Syntax

The command takes a single required argument that specifies the desired state for the airplane mode.

The following example enables airplane mode:

```yaml
- setAirplaneMode: enabled
```

The following example disables airplane mode:

```yaml
- setAirplaneMode: disabled
```

### Related commands

* [toggleairplanemode.md](toggleairplanemode.md "mention")
