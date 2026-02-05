---
description: Automatically scroll until a target element becomes visible on screen.
---

# scrollUntilVisible

Scrolls the screen in a specified direction until a target element is visible.

### Parameters

The following parameters configure the `scrollUntilVisible` command.

<table><thead><tr><th width="199">Parameter</th><th width="124">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>element</code></td><td><code>string</code> or <code>object</code></td><td><strong>Required.</strong> The selector for the element to find. To select the element, you can use any of the available selectors.</td></tr><tr><td><code>direction</code></td><td><code>string</code></td><td><strong>(Optional).</strong> The direction to scroll. Accepts <code>DOWN</code>, <code>UP</code>, <code>LEFT</code>, or <code>RIGHT</code>. Defaults to <code>DOWN</code>.</td></tr><tr><td><code>timeout</code></td><td><code>integer</code></td><td><strong>(Optional).</strong> The maximum time in milliseconds to scroll while searching for the element. If the timeout is reached before the element is found, the test fails. Defaults to <code>20000</code> milliseconds.</td></tr><tr><td><code>speed</code></td><td><code>integer</code></td><td><strong>(Optional).</strong> The scroll speed, specified as a value from <code>0</code> to <code>100</code>. Higher values result in faster scrolling. Defaults to <code>40</code>.</td></tr><tr><td><code>visibilityPercentage</code></td><td><code>integer</code></td><td><strong>(Optional).</strong> The percentage of the element, from <code>0</code> to <code>100</code>, that must be visible in the viewport for the scroll to stop. Defaults to <code>100</code>.</td></tr><tr><td><code>centerElement</code></td><td><code>boolean</code></td><td><strong>(Optional).</strong> If <code>true</code>, the command keeps scrolling until the element is more than 30% away from the viewport edge (e.g. in the top 70% when scrolling down). If the element cannot reach that position (e.g. it is the last list item), the command stops after a few attempts. Defaults to <code>false</code>.</td></tr></tbody></table>

{% hint style="info" %}
By default, an element is considered visible if it is fully displayed in the viewport.
{% endhint %}

#### How it works

The command checks whether the target element is visible. If not, it swipes from the center of the screen toward the edge (to 10% from the edge in the chosen direction), checks again, and repeats until the element is found or the timeout is reached.

This behavior works well when the whole screen scrolls (e.g. a full-screen list). When only part of the screen is scrollable (such as a bottom sheet, a fragment, or a small widget), the swipe may miss the scrollable region. For those layouts, use a custom scroll loop; see [Custom scrolling for screen fragments](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/examples/custom-scrolling-for-screen-fragments).

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

Use `centerElement: true` to keep scrolling until the target is not only visible but also more than 30% away from the viewport edge. The example below stops when "Item 6" meets that condition.

```yaml
- scrollUntilVisible:
    centerElement: true
    element:
      text: "Item 6"
```
