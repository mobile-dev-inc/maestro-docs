---
description: Enable airplane mode to test offline behavior.
---

# setAirplaneMode

The `setAirplaneMode` command enables or disables airplane mode on the device.&#x20;

{% hint style="info" %}
This command is supported on Android only.

iOS simulators do not have an airplane mode.

On web or iOS, the command will pass but has no effect.
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
