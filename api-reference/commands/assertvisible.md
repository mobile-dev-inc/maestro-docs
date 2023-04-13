# assertVisible

To assert whether an element is **visible**, use the following command that takes the same parameters as `tapOn`

```yaml
- assertVisible:
    # Same exact parameters as in Tap On View
```

This command will wait for view to appear if it is not visible yet.

You are most likely going to be using the following properties, but please refer to the [Selectors](../selectors.md) page for an exhaustive list of all available selectors:

* `text` - text in a view
* `id` - id of a view
* `enabled` - `true` if view is enabled
* `checked` - `true` if view is checked
* `focused` - `true` if view has keyboard focus
* `selected` - `true` if view is selected

#### Example

To check whether view with a text `My Button` is visible **and** enabled you can run the following command:

```yaml
- assertVisible:
    text: My Button
    enabled: true
```

Such test will fail if _either_

* There is no button with such text
* There is a button but it is disabled
