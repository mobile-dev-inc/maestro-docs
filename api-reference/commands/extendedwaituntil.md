---
description: Wait for elements to appear or disappear with timeout in Maestro.
---

# extendedWaitUntil

Waits until an element becomes visible. Fails if the element is not visible after the timeout expires. This command will complete as soon as element becomes visible and is not going to wait for timeout to expire.

For an exhaustive list of selectors that can be used, please refer to the [Selectors](../selectors.md) page.

Example usage:

```yaml
- extendedWaitUntil:
    visible: "My text that should be visible" # or any other selector
    timeout: 10000      # Timeout in milliseconds
```

Similarly, it can wait until an element disappears:

```yaml
- extendedWaitUntil:
    notVisible: 
        id: "elementId" # or any other selector
    timeout: 10000
```

#### See also

{% content-ref url="../../advanced/wait.md" %}
[wait.md](../../advanced/wait.md)
{% endcontent-ref %}
