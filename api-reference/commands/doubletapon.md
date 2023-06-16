# doubleTapOn

It will double tap on a selected element or point.&#x20;

```yaml
- doubleTapOn: "Button"
```

Accepts the same element selectors as tapOn

```yaml
- doubleTapOn:
    id: "someId" # or any other selector
    delay: 100 # (optional) Delay between taps. Default, 100ms
```

### Example

```
appId: com.other.app
---
- launchApp
- doubleTapOn:
    id: buttonId
```
