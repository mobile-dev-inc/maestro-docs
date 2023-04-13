# tapOn

Taps on a view on the screen using a selector:

```yaml
- tapOn:
    text: "Text"     # (optional) Finds text that matches regexp
    id: "id"         # (optional) Finds id that matches regexp
    # or any other selector
```

For a full list of selectors, please refer to the [Selectors](../selectors.md) page.

### Tapping on a specific point on the screen

{% hint style="info" %}
Whenever possible, prefer tapping on view id or text instead of coordinates as this might make your tests dependent on a specific type of a device
{% endhint %}

You can specify a relative position on the screen using:

```yaml
- tapOn:
    point: 0%,0%        # top-left corner
- tapOn:
    point: 100%,100%    # bottom-right corner
- tapOn:
    point: 50%,50%      # middle of the screen
```

You can also specify absolute coordinates on the screen to tap on:

```yaml
- tapOn:
    point: 100,200    # This command will tap on point x:100 y:200 on the screen (in pixels)
```

### Long press

To long press on a view or a point, use the same exact properties but with a `longPressOn` command

```yaml
- longPressOn: Text
- longPressOn:
    id: view_id
- longPressOn:
    point: 50%,50%
```

### Selecting one view among many similar

If you have multiple views matching the same selector (i.e. many views with text `Hello`), use `index` parameter to specify which one to select exactly. For example, the following command will pick the **3rd view** that has text `Hello`:

```yaml
- tapOn:
    text: Hello
    index: 2
```

## Example

```yaml
appId: com.android.contacts
---
- launchApp
- tapOn:
    id: .*floating_action_button.* #regex
- inputText: "John"
- tapOn: "Last Name"
- inputText: "Snow"
- tapOn: .*Save.*
```
