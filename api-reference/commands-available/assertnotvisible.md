---
description: Assert that a UI element is not present or visible on the screen.
---

# assertNotVisible

The `assertNotVisible` command asserts that a UI element is not visible on the screen. If the element is currently visible, this command waits for it to disappear before proceeding.

{% hint style="info" %}
#### Maestro's fluent assertion

If the element is visible when the command is first called, Maestro will not immediately fail the test. Instead, it will automatically wait and retry for up to 7 seconds, giving the UI time to update or for animations to complete.

If you expect an element to take longer than 7 seconds to disappear, use the [`extendedWaitUntil`](extendedwaituntil.md) command.
{% endhint %}

### Parameters

This command accepts the same selectors as `tapOn`. The following table lists commonly used parameters.

| Parameter  | Type      | Description                                                            |
| ---------- | --------- | ---------------------------------------------------------------------- |
| `text`     | `string`  | The text content of the element.                                       |
| `id`       | `string`  | The ID of the element.                                                 |
| `enabled`  | `boolean` | Specifies if the element is enabled (`true`) or disabled (`false`).    |
| `checked`  | `boolean` | Specifies if the element is checked (`true`) or unchecked (`false`).   |
| `focused`  | `boolean` | Specifies if the element has keyboard focus (`true`) or not (`false`). |
| `selected` | `boolean` | Specifies if the element is selected (`true`) or not (`false`).        |

For a complete list of all available selectors, see the [Selectors](../selectors/) reference.

### Usage examples

The following examples demonstrate how to use `assertNotVisible`.

#### Assert an element with specific text is not visible

This example uses the shorthand syntax to assert that an element with the text `My Button` is not on the screen.

```yaml
- assertNotVisible: "My Button"
```

#### Assert an element matching multiple properties is not visible

This example asserts that an enabled element with the text `My Button` is not visible. The command passes if no visible element matches both the `text` and `enabled` criteria. The test only fails if an element that is both enabled and has the text `My Button` is currently visible on the screen.

```yaml
- assertNotVisible:
    text: "My Button"
    enabled: true
```

### Related commands

* [`assertVisible`](assertvisible.md)
* [`assertTrue`](asserttrue.md)
