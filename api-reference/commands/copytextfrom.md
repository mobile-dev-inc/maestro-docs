# copyTextFrom

You can copy text from an element and save it in-memory, to paste later. To find the element, use the syntax below:

```yaml
- copyTextFrom:
    text: "Text"     # (optional) Finds element with text that matches regexp
    id: "id"         # (optional) Finds element with id that matches regexp
    index: 0         # (optional) 0-based index of the view to select among those that match all other criteria
    width: 100       # (optional) Finds element of a given width
    height: 100      # (optional) Finds element of a given height
    tolerance: 10    # (optional) Tolerance to apply when comparing width and height
    enabled: true    # (optional) Searches for view with a given "enabled" state
    optional: false  # (default: false) If set to true, test won't fail if view can't be found
    below: "View above that has this text"     # This will match view *above* that has the given text
    above:
        id: "view_below_id"                    # This will match a view *below* that has the given id
    leftOf: "View to the right has this text"
    rightOf: "View to the left has this text"
    containsChild: "Text in a child view"      # This will match a view that has a *direct* child view with the given text
```

### Usage Example

Copies text from an element and pastes it into a search field.

```
appId: com.example.app
---
- launchApp
- copyTextFrom:
    id: "someId"
- tapOn:
    id: "searchFieldId"
- pasteText
```
