---
description: Toggle dark mode on or off during test execution.
---

# toggleDarkMode

Toggles the device's system-wide dark mode (light/dark appearance) state.

{% hint style="info" %}
On Android, this toggles the system night mode setting. On iOS, this requires iOS 15+ and controls the simulator's system appearance. On web, the command will pass but has no effect.
{% endhint %}

### Syntax

This command takes no arguments.

```yaml
- toggleDarkMode
```

### Related commands

* [setdarkmode.md](setdarkmode.md "mention")
