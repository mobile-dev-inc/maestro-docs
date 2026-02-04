---
description: Toggle airplane mode on or off during test execution.
---

# toggleAirplaneMode

Toggles the device's airplane mode on or off.

{% hint style="info" %}
This command is only useful on Android. iOS simulators do not have an airplane mode. On iOS or web, the command will pass but has no effect.
{% endhint %}

### Syntax

This command takes no arguments.

```yaml
- toggleAirplaneMode
```

### Platform availability

This command is supported on Android only. iOS simulators do not have an airplane mode.

### Related commands

* [setairplanemode.md](setairplanemode.md "mention")
