---
description: Perform a double-tap gesture on a UI element or screen coordinates.
---

# doubleTapOn

Double-taps a UI element or a specific point on the screen.

### Arguments

The `doubleTapOn` command accepts a [Selector](../selectors/) and a `delay` :

| Argument                  | Description                                                                                                                                                                                               |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Selector](../selectors/) | The element to double-tap. This can be a string representing the element's text, the accessibility ID, or an object specifying a selector. Accepts the same selectors as the [`tapOn`](tapon.md) command. |
| `delay`                   | (Optional) The delay in milliseconds between the first and second tap. Defaults to `100`.                                                                                                                 |

### Usage examples

You can use the shorthand approach by providing the visible text of the element. This example double-taps an element with the visible text `My Button`:

```yaml
- doubleTapOn: My Button
```

The implementation above produces the same result as using [`tapOn`](tapon.md) with the `repeat` configuration.

```yaml
- tapOn:
    text: My Button
    repeat: 2
    delay: 100
```

If you need to use a different selector, or if you need to change the delay between the first and second tap, use this approach. This example uses an `id` selector to find the element and specifies a custom delay between taps:

```yaml
- doubleTapOn:
    id: "someId"
    delay: 200
```

### Related commands

* [tapon.md](tapon.md "mention")
