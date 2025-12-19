---
description: >-
  Confirm element visibility with assertVisible, waiting for appearance and
  state checks.
---

# assertVisible

To assert whether an element is **visible**, use the following command that takes the same parameters as `tapOn`

```yaml
- assertVisible:
    # Same exact parameters as in tapOn or any other command that uses selectors
```

This command will wait for view to appear if it is not visible yet.

You are most likely going to be using the following properties, but please refer to the [Selectors](../selectors.md) page for an exhaustive list of all available selectors:

* `text` - text in a view
* `id` - id of a view
* `enabled` - `true` if view is enabled
* `checked` - `true` if view is checked
* `focused` - `true` if view has keyboard focus
* `selected` - `true` if view is selected

#### Examples

To check whether view with a text `My Button` is visible you can run the following command:

```yaml
- assertVisible: "My Button"
```

To check whether view with a text `My Button` is visible **and** enabled you can run the following command:

```yaml
- assertVisible:
    text: "My Button"
    enabled: true
```

Such test will fail if _either_

* There is no button with such text
* There is a button but it is disabled

#### Related commands

{% content-ref url="assertnotvisible.md" %}
[assertnotvisible.md](assertnotvisible.md)
{% endcontent-ref %}

{% content-ref url="asserttrue.md" %}
[asserttrue.md](asserttrue.md)
{% endcontent-ref %}
