# scrollUntilVisible

Scrolls the screen in a specified direction until a target element is visible.

### Parameters

The following parameters configure the `scrollUntilVisible` command.

<table><thead><tr><th width="200">Parameter</th><th width="108.4444580078125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>element</code></td><td><code>string</code> or <code>object</code></td><td><strong>Required.</strong> The selector for the element to find. To select the element, you can use any of the available selectors.</td></tr><tr><td><code>direction</code></td><td><code>string</code></td><td><strong>(Optional)</strong><em>.</em> The direction to scroll. Accepts <code>DOWN</code>, <code>UP</code>, <code>LEFT</code>, or <code>RIGHT</code>. Defaults to <code>DOWN</code>.</td></tr><tr><td><code>timeout</code></td><td><code>integer</code></td><td><strong>(Optional)</strong><em>.</em> The maximum time in milliseconds to scroll while searching for the element. If the timeout is reached before the element is found, the test fails. Defaults to <code>20000</code> milliseconds.</td></tr><tr><td><code>speed</code></td><td><code>integer</code></td><td><strong>(Optional)</strong><em>.</em> The scroll speed, specified as a value from <code>0</code> to <code>100</code>. Higher values result in faster scrolling. Defaults to <code>40</code>.</td></tr><tr><td><code>visibilityPercentage</code></td><td><code>integer</code></td><td><strong>(Optional)</strong><em>.</em> The percentage of the element, from <code>0</code> to <code>100</code>, that must be visible in the viewport for the scroll to stop. Defaults to <code>100</code>.</td></tr><tr><td><code>centerElement</code></td><td><code>boolean</code></td><td><strong>(Optional)</strong><em>.</em> If <code>true</code>, the command attempts to position the element more than 30% away from the edge of the screen (e.g. scrolling stops when the target is in the top 70% of the viewport). If the element cannot be centered (for example, it is the last item in a list), the scroll stops after a few attempts. Defaults to <code>false</code>.</td></tr></tbody></table>

{% hint style="info" %}
By default, an element is considered visible if it is fully displayed in the viewport.
{% endhint %}

#### Implementation details

`scrollUntilVisible` is a convenience wrapper for an algorithm built from other Maestro commands:

1. **Visibility check** — Assert whether the target element is visible.
2. **If visible** — The command ends.
3. **If not visible** — The device swipes from the centre of the screen to 10% from the edge in the chosen direction, then checks visibility again.
4. **Loop** — Steps 2–3 repeat until the element is found or the `timeout` is reached.

This centre-based swipe works well for full-screen lists. When only part of the screen is scrollable (e.g. a bottom sheet, a scrollable fragment, or a small widget), the default behaviour may not hit the scrollable area. In those cases, you can implement custom scroll logic; see Custom scrolling for screen fragments for an example.

### Usage examples

The following examples demonstrate how to use the `scrollUntilVisible` command.

#### Scroll to an element with specific text

This example scrolls down until an element containing the text "My text" is visible.

```yaml
- scrollUntilVisible:
    element: "My text"
    direction: DOWN
```

#### Scroll to an element by ID

This example scrolls down until a view with a matching ID becomes visible.

```yaml
- scrollUntilVisible:
    element:
      id: ".*some_view_id"
    direction: DOWN
```

#### Center an element after scrolling

With `centerElement: true`, the command scrolls until the target is visible and then keeps scrolling until the element is more than 30% away from the edge (e.g. in the top 70% of the viewport when scrolling down). This example stops when "Item 6" satisfies that condition.

```yaml
- scrollUntilVisible:
    centerElement: true
    element:
      text: "Item 6"
```
