---
description: Assert that a UI element is visible on screen with automatic retry.
---

# assertVisible

The `assertVisible` command asserts that a UI element is visible on the screen. If the element is not immediately visible, this command waits for it to appear before timing out.

{% hint style="info" %}
#### Maestro's fluent assertion

If the element is not visible when the command is first called, Maestro will not immediately fail the test. Instead, it will automatically wait and retry for up to 7 seconds, giving the UI time to update or for animations to complete.

If you expect an element to take longer than 7 seconds to appear, use the [`extendedWaitUntil`](extendedwaituntil.md) command.
{% endhint %}

### Parameters

The `assertVisible` command uses a selector to identify the target UI element. You can specify the selector as a single string (shorthand for the `text` property) or as a YAML object with multiple properties.

The following table lists common selector properties. For a complete list of all available selectors, see the [Selectors](https://docs.maestro.dev/api-reference/selectors) documentation.

| Selector   | Description                                                            |
| ---------- | ---------------------------------------------------------------------- |
| `text`     | The text content of the element.                                       |
| `id`       | The ID of the element.                                                 |
| `enabled`  | Specifies if the element is enabled (`true`) or disabled (`false`).    |
| `checked`  | Specifies if the element is checked (`true`) or unchecked (`false`).   |
| `focused`  | Specifies if the element has keyboard focus (`true`) or not (`false`). |
| `selected` | Specifies if the element is selected (`true`) or not (`false`).        |

### Usage examples

#### Assert an element is visible by its text

This example asserts that an element containing the text `My Button` is visible on the screen.

```yaml
- assertVisible: "My Button"
```

#### Assert an element is visible and enabled

This example asserts that an element with the text `My Button` is both visible and enabled.

```yaml
- assertVisible:
    text: "My Button"
    enabled: true
```

The command fails if either of the following conditions is true:

* No element with the text `My Button` is found.
* An element with the text `My Button` is found, but it is disabled.

### Related commands

* [assertnotvisible.md](assertnotvisible.md "mention")
* [asserttrue.md](asserttrue.md "mention")
