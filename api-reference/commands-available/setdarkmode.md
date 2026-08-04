---
description: Enable or disable dark mode to test light/dark UI behavior.
---

# setDarkMode

The `setDarkMode` command sets the system-wide dark mode (light/dark appearance) state on the device.

{% hint style="info" %}
On Android, this toggles the system night mode setting. On iOS, this requires iOS 15+ and controls the simulator's system appearance. On web, this forces the `prefers-color-scheme` media query, which affects any page using it to detect dark mode.
{% endhint %}

### Syntax

The command takes a single required argument that specifies the desired state for dark mode.

The following example enables dark mode:

```yaml
- setDarkMode: enabled
```

The following example disables dark mode:

```yaml
- setDarkMode: disabled
```

### Related commands

* [toggledarkmode.md](toggledarkmode.md "mention")
