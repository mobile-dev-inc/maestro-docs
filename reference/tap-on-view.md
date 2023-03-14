# Tap On View

Taps on a view on the screen:

```yaml
- tapOn:
    text: "Text"     # (optional) Finds text that matches regexp
    id: "id"         # (optional) Finds id that matches regexp
    index: 0         # (optional) 0-based index of the view to select among those that match all other criteria
    width: 100       # (optional) Finds element of a given width
    height: 100      # (optional) Finds element of a given height
    tolerance: 10    # (optional) Tolerance to apply when comparing width and height
    enabled: true    # (optional) Searches for view with a given "enabled" state
    checked: true    # (optional) Searches for view with a given "checked" state
    focused: true    # (optional) Searches for view with a given "focused" state
    selected: true   # (optional) Searches for view with a given "selected" state
    optional: false  # (default: false) If set to true, test won't fail if view can't be found
```

### Relative Position

Maestro is also able to select views using their relative position (i.e. "below another view", or "contains child")

```yaml
- tapOn:
    below: "View above that has this text"     # This will match view *above* that has the given text
    above:
        id: "view_below_id"                    # This will match a view *below* that has the given id
    leftOf: "View to the right has this text"
    rightOf: "View to the left has this text"
    containsChild: "Text in a child view"      # This will match a view that has a *direct* child view with the given text
```

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
