# assertNotVisible

The `assertNotVisible` command asserts that a UI element is not visible on the screen. If the element is currently visible, this command waits for it to disappear before proceeding.

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
