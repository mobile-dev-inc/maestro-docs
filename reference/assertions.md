# Assertions

### assertVisible

To assert whether an element is **visible**, use the following command that takes the same parameters as `tapOn`

```yaml
- assertVisible:
    # Same exact parameters as in Tap On View
```

This command will wait for view to appear if it is not visible yet.

{% content-ref url="tap-on-view.md" %}
[tap-on-view.md](tap-on-view.md)
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
- assertVisible:
    text: My Button
    enabled: true
```

Such test will fail if _either_

* There is no button with such text
* There is a button but it is disabled

### assertNotVisible

To assert whether an element is **not visible**, use the following command that takes the same parameters as `tapOn`

```yaml
- assertNotVisible:
    # Same exact parameters as in Tap On View
```

If a view is currently visible, this command will wait for the view to disappear.

### assertTrue

Asserts whether given value is either true or non-empty (or _truthy_ in Javascript terms):

```yaml
- assertTrue: ${value}
```

This command is primarily designed to be used in combination with Javascript values. I.e. asserting that text between two views matches:

```yaml
- copyTextFrom: View A
- evalScript: ${output.viewA = maestro.copiedText}
- copyTextFrom: View B
- assertTrue: ${output.viewA == maestro.copiedText}
```

{% content-ref url="../advanced/javascript/" %}
[javascript](../advanced/javascript/)
{% endcontent-ref %}
