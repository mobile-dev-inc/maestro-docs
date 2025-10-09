---
description: >-
  Use the tapOn command in Maestro to tap by text or ID, repeat taps, adjust
  wait times, and handle retries for reliable UI test interactions.
---

# tapOn

In order to tap on a view with the text "My text" you can use the shorthand selector for text like this:

```yaml
- tapOn: "My text"
```

You can also use other selectors such as id:

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

### retryTapIfNoChange

Sometimes, a tap will occur too early because an API request is happening and the app isn't ready for the tap. To fix such cases, use retryTapIfNoChange. For example:

```yaml
- tapOn:
    id: "someId"
    retryTapIfNoChange: true
```

In this example, the tapOn will try to tap again if the screen hierarchy doesn't change after the first tap.

### Control wait time

Maestro usually waits for the screen to settle before moving to the next command, however that is not always desirable.

If your app or screen has the following:

* Moving elements like a countdown timer
* Non-blocking animations that are part of the UI

Then, you can use `waitToSettleTimeoutMs` to limit the time Maestro waits for things to settle

```yaml
- tapOn:
    text: "Button"
    waitToSettleTimeoutMs: 500 # ms
```

**Note:** This will be a best effort timeout. Maestro will not interrupt core operations to honor the timeout.

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
