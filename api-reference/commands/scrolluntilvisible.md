# scrollUntilVisible

To scroll towards a direction until an element becomes visible in the view hierarchy, use the following command:

<pre class="language-yaml"><code class="lang-yaml"><strong>- scrollUntilVisible:
</strong>    element:
      id: "viewId" # or any other selector
    direction: DOWN # DOWN|UP|LEFT|RIGHT (optional, default: DOWN)
    timeout: 50000 # (optional, default: 20000ms)
    speed: 40 # 0-100 (optional, default: 40) Scroll speed. Higher values scroll faster.
    visibilityPercentage: 100 # 0-100 (optional, default 100) Percentage of element visible in viewport
</code></pre>

Please refer to the [Selectors](../selectors.md) page for a full list of supported selectors.

#### Direction

The scroll will move towards the direction specified `DOWN|UP|LEFT|RIGHT`. For example, if `DOWN` is specified then it will start scrolling towards the bottom of the screen.

#### Visibility Percentage

By default an element will be considered visible if it is fully displayed in the viewport. You can adjust that threshold by modifying `visibilityPercentage`.

#### Example

If we want to scroll towards the bottom until a view with id `com.example.resource.some_view_id` becomes visible:

```yaml
- scrollUntilVisible:
    element:
      id: ".*some_view_id"
    direction: DOWN
```
