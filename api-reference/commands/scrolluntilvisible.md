# scrollUntilVisible

To scroll towards a direction until an element becomes visible in the view hierarchy, use the following command:

<pre class="language-yaml"><code class="lang-yaml"><strong>- scrollUntilVisible:
</strong>    element:
      id: "viewId" # or any other selector
    direction: DOWN # DOWN|UP|LEFT|RIGHT (optional, default: DOWN)
    timeout: 50000 # (optional, default: 20000) ms
    speed: 40 # 0-100 (optional, default: 40) Scroll speed. Higher values scroll faster.
    visibilityPercentage: 100 # 0-100 (optional, default: 100) Percentage of element visible in viewport
    centerElement: false # true|false (optional, default: false)
</code></pre>

Please refer to the [Selectors](../selectors.md) page for a full list of supported selectors.

### Direction

The scroll will move towards the direction specified `DOWN|UP|LEFT|RIGHT`. For example, if `DOWN` is specified then it will start scrolling towards the bottom of the screen.



### Center Element

If enabled, it will attempt to stop when the element is closer to the screen center.&#x20;

In case it's not possible to bring the element to the center (i.e it's the last element in the list), it will stop scrolling after few attempts.

```yaml
- scrollUntilVisible:
    centerElement: true
    element:
      text: "Item 6"
```



### Visibility Percentage

By default an element will be considered visible if it is fully displayed in the viewport. You can adjust that threshold by modifying `visibilityPercentage`.



### Example

If you want to scroll until the text "My text" is visible you can run the following command:

```yaml
- scrollUntilVisible:
    element: "My text" # or any other selector
    direction: DOWN
```

If we want to scroll towards the bottom until a view with id `com.example.resource.some_view_id` becomes visible, you can use the `id` selector like this:

```yaml
- scrollUntilVisible:
    element:
      id: ".*some_view_id" # or any other selector
    direction: DOWN
```

