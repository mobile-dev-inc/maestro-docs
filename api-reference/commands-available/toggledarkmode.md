---
description: Toggle dark mode on or off during test execution.
---

# toggleDarkMode

Toggles the device's system-wide dark mode (light/dark appearance) state.

{% hint style="info" %}
On Android, this toggles the system night mode setting. On iOS, this controls the simulator's system appearance. On web, this forces the `prefers-color-scheme` media query, which affects any page using it to detect dark mode.
{% endhint %}

### Syntax

This command takes no arguments.

```yaml
- toggleDarkMode
```

### Related commands

* [setdarkmode.md](setdarkmode.md "mention")
* [assertdarkmode.md](assertdarkmode.md "mention")
* [assertlightmode.md](assertlightmode.md "mention")
