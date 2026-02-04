---
description: Long press on elements for context menus or drag-and-drop operations.
---

# longPressOn

The `longPressOn` command performs a long press (3 seconds) gesture on a UI element. It is the long-press equivalent of the [`tapOn` ](tapon.md)command.

### Usage examples

The `longPressOn` command accepts the same properties as `tapOn`, including [Selectors](../selectors/). The following examples demonstrate how to long press on text, an ID, or a point coordinates:

```yaml
- longPressOn: Text
- longPressOn:
    id: view_id
- longPressOn:
    point: 50%,50%
```

#### Long press on a specific point within an element

To long press on a specific point relative to an element, combine the selector with a `point` property. The following example finds an element containing the text "A text with a hyperlink" and performs a long press at the coordinates `90%,50%` within that element's bounds (effectively targeting the end of the sentence).

```yaml
- longPressOn:
    text: "A text with a hyperlink"
    point: "90%,50%"
```

### Related commands

* [tapon.md](tapon.md "mention")
