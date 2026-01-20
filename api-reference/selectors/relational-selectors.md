# Relational Selectors

Relational Selectors allow you to identify UI elements based on their relationship to other views on the screen. This is extremely useful when elements have generic names (like multiple "Buy" buttons) or when you want to target a view that lacks a stable `text` or `id` but is always located near a known anchor.

### **Overview**

| **Selector**          | **Description**                                                              |
| --------------------- | ---------------------------------------------------------------------------- |
| `above`               | Matches a view located vertically above a specified anchor element.          |
| `below`               | Matches a view located vertically below a specified anchor element.          |
| `leftOf`              | Matches a view located to the left of a specified anchor element.            |
| `rightOf`             | Matches a view located to the right of a specified anchor element.           |
| `containsChild`       | Matches a parent element that has a direct child matching specific criteria. |
| `childOf`             | Matches an element that is a child of a specified parent element.            |
| `containsDescendants` | Matches a view that contains a specific set of descendant views.             |

{% hint style="success" %}
#### Usage tips

* **Compound Selectors**:  Positional selectors can be combined with other selector attributes (`id`, `text`, `enabled`, etc.) for higher precision. For example, `tapOn: { id: "icon", rightOf: "Settings", enabled: true }`.
* **Anchor Reliability**:  Always use the most stable element (typically static text or a unique ID) as the anchor for `above`, `below`, `leftOf`, or `rightOf`.
{% endhint %}

### Vertical Alignment: `above` and `below`

These selectors identify views located above or below a reference element.

```yaml
# Tap a view located below the "Email" label
- tapOn:
    below: Email

# Tap a view located above the "Checkout" title
- tapOn:
    above: Checkout
```

### Horizontal Alignment: `leftOf` and `rightOf`

Use these selectors for elements positioned side-by-side, such as icons next to labels.

```yaml
# Tap the view to the right of an input field
- tapOn:
    rightOf:
      id: input_text

# Tap the view to the left of a specific phrase
- tapOn:
    leftOf: I agree to the terms
```

### Parent-Child Relationships

These selectors navigate the accessibility tree rather than relying on screen position.

#### `containsChild` (Direct child only)

This matches a parent element that has a direct child matching the given selector.

```yaml
# Tap the container that directly contains the text "Order 12345"
- tapOn:
    containsChild:
      text: Order 12345
```

#### `childOf` (Direct parent only)

This matches an element that is a direct child of a specific parent. This is useful when the same child element exists in multiple containers.

```yaml
# Tap the Delete button inside the Basket
- tapOn:
    text: Delete
    childOf:
        id: basket_container
```

#### **`containsDescendants`**

This matches a view that contains all specified descendant elements, at any depth in its hierarchy. This is not limited to direct children. Use `containsDescendants` for complex components like cards, rows, or grouped layouts where relevant elements may be nested multiple levels deep.

```yaml
# Find a list item that contains both a specific product name and a price
- assertVisible:
    id: list_item
    containsDescendants:
      - text: Wireless Headphones
      - text: $99.99
```
