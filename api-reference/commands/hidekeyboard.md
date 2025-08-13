---
description: Hide virtual keyboard in Maestro tests; note potential instability on iOS.
---

# hideKeyboard

### hideKeyboard

To hide the software keyboard, use `hideKeyboard` command:

```yaml
- hideKeyboard
```

{% hint style="warning" %}
On iOS, hideKeyboard can be flaky. [Read more here](../../troubleshooting/known-issues.md#ios-hidekeyboard-flaky).
{% endhint %}
