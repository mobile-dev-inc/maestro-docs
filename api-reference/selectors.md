# Selectors

For commands that interact with a view, such as tapOn, assertVisible, copyTextFrom among others, require the view to be found using what is called a _selector_. There are many different selectors available for usage:

```yaml
- tapOn: # or any other command that works with selectors
    text: "Text"     # (optional) Finds text or accessibility text that matches regexp. 
    id: "id"         # (optional) Finds id that matches regexp
    index: 0         # (optional) 0-based index of the view to select among those that match all other criteria
    point: 50%,50%.  # (optional) Relative position on screen. 50%,50%: Middle of screen
    point: 50, 50    # (optional) Exact coordinates on screen, x:50 y:50, in pixels.
    width: 100       # (optional) Finds element of a given width
    height: 100      # (optional) Finds element of a given height
    tolerance: 10    # (optional) Tolerance to apply when comparing width and height
    enabled: true    # (optional) Searches for view with a given "enabled" state
    checked: true    # (optional) Searches for view with a given "checked" state
    focused: true    # (optional) Searches for view with a given "focused" state
    selected: true   # (optional) Searches for view with a given "selected" state
    optional: false  # (default: false) If set to true, test won't fail if view can't be found
```

### Shorthand selector for text

If you want to use the text selector you can use the shorthand selector like this:

```yaml
- tapOn: "Text" # or any other command that works with selectors
```

### Relative Position selectors

Apart from the selectors mentioned above, Maestro is also able to select views using their relative position (i.e. "below another view", or "contains child")

```yaml
- tapOn: # or any other command that works with selectors
    below: "View above that has this text"     # This will match view *above* that has the given text
    above:
        id: "view_below_id"                    # This will match a view *below* that has the given id
    leftOf: "View to the right has this text"
    rightOf: "View to the left has this text"
    containsChild: "Text in a child view"      # This will match a view that has a *direct* child view with the given text
    childOf:                                   # This will help to select from children of view with id 'buy-now'
        - id: "buy-now"
    containsDescendants:                       # This will match a view that has all the descendant views given below
        - id: "title_id"
          text: "A descendant view has id 'title_id' and this text"
        - "Another descendant view has this text"
```

### Selecting one view among many similar

If you have multiple views matching the same selector (i.e. many views with text `Hello`), use `index` parameter to specify which one to select exactly. For example, the following command will pick the **3rd view** that has text `Hello`:

```yaml
- tapOn:
    text: Hello
    index: 2
```
