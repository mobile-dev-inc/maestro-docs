# tapOn

In order to tap on a view with the text "My text" you can use the shorthand selector for text like this:

```yaml
- tapOn: "My text"
```

You can also use other selectors such as id:&#x20;

```yaml
- tapOn:
    id: "id" # or any other selector
```

For a full list of selectors, please refer to the [Selectors](../selectors.md) page.

### Repeat taps

In some cases it is desirable to repeat taps. To achieve that, the following is possible:

```yaml
- tapOn:
    text: "Button"
    repeat: 3
    delay: 500 # (optional) Delay between taps. Default 100ms

- tapOn:
    id: "someId"
    repeat: 3
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

### Tapping on a specific point within another element

If you wish to tap on a point on screen inside another element you can do the following:

```
- tapOn:
    text: "A text with a hyperlink"
    point: "90%,50%"
```

This will find an element with text "A text with a hyperlink" and tapOn towards the end of the sentence where "hyperlink" is located.

### Long press

To long press on a view or a point, use the same exact properties but with a `longPressOn` command:

```yaml
- longPressOn: Text
- longPressOn:
    id: view_id
- longPressOn:
    point: 50%,50%
```

### Long press on a specific point within another element

If you wish to long press on a point on screen inside another element you can do the following:

```
- longPressOn:
    text: "A text with a hyperlink"
    point: "90%,50%"
```

This will find an element with text "A text with a hyperlink" and longPressOn towards the end of the sentence where "hyperlink" is located.

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
