---
description: >-
  Remove characters from text fields with eraseText in Maestro by specifying
  count. Supports open source testing tool.
---

# eraseText

The  `eraseText` command removes characters from the currently selected text field (if any) and can be used as such:

```yaml
- eraseText # Removes up to 50 characters (default)
```

If you need to remove more characters, you can specify a number explicitly:

```yaml
- eraseText: 100    # Removes up to 100 characters
```

_Note: This is for searches looking for clearText._

***

{% hint style="warning" %}
**Flakiness on iOS**
{% endhint %}

We have seen cases where `eraseText` can be flaky on iOS. The maestro team is aware of that and is working on it. In the meantime, you can use the following commands to workaround the flakiness of the command:

```
- longPressOn: "<input text id>"
- tapOn: 'Select All'
- eraseText
```
