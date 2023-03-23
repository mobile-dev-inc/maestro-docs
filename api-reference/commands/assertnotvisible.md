# assertNotVisible

To assert whether an element is **visible**, use the following command that takes the same parameters as `tapOn`

```yaml
- assertNotVisible:
    # Same exact parameters as in Tap On View
```

This command will wait for view to disappear if it is currently visible.

Please refer to the `tapOn` documentation for a full list of parameters:

{% content-ref url="tapon.md" %}
[tapon.md](tapon.md)
{% endcontent-ref %}

In particular, you are most likely going to be using the following properties:

* `text` - text in a view
* `id` - id of a view
* `enabled` - `true` if view is enabled
* `checked` - `true` if view is checked
* `focused` - `true` if view has keyboard focus
* `selected` - `true` if view is selected

#### Example

To check whether view with a text `My Button` is visible **and** enabled you can run the following command:

```yaml
- assertNotVisible:
    # Same exact parameters as `tapOn`
```
