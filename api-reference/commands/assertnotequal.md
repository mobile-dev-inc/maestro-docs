---
description: Assert that two values are not equal in Maestro flows.
---

# assertNotEqual

Asserts that two values are not equal after JavaScript evaluation:

```yaml
- assertNotEqual:
    value1: "foo"
    value2: "bar"
```

This command compares `value1` and `value2` as strings after evaluating any JavaScript expressions. If the values are equal, the assertion fails.

### Basic usage

Ensure a value is not a specific string:

```yaml
- assertNotEqual:
    value1: ${output.status}
    value2: "error"
```

Verify UI text has changed:

```yaml
- copyTextFrom:
    id: "counter"
- evalScript: ${output.initialCount = maestro.copiedText}
- tapOn: "Increment"
- copyTextFrom:
    id: "counter"
- assertNotEqual:
    value1: ${maestro.copiedText}
    value2: ${output.initialCount}
    label: "Counter should have changed"
```

### With label and optional

```yaml
- assertNotEqual:
    value1: ${output.userId}
    value2: ""
    label: "User ID should not be empty"
    optional: true
```

### Use in conditions

`assertNotEqual` can be used in `runFlow` and `repeat` conditions:

```yaml
- runFlow:
    when:
      notEqual:
        value1: ${output.status}
        value2: "disabled"
    commands:
      - tapOn: "Submit"
```

```yaml
- repeat:
    while:
      notEqual:
        value1: ${output.loading}
        value2: "false"
    commands:
      - waitForAnimationToEnd
```

### Considerations

`assertNotEqual` compares values as strings after JavaScript evaluation:

- **Numbers are normalized**: `${1}` and `${1.0}` both evaluate to `"1"` and will match
- **Booleans become strings**: `${true}` evaluates to `"true"`

This means `${true}` and `${1}` are not considered equal — they evaluate to `"true"` and `"1"` respectively. If you need JavaScript type coercion, for e.g. where `1 == true`, use `assertTrue`:

```yaml
- assertTrue: ${1 == true}
```

### Related commands

{% content-ref url="assertequal.md" %}
[assertequal.md](assertequal.md)
{% endcontent-ref %}

{% content-ref url="asserttrue.md" %}
[asserttrue.md](asserttrue.md)
{% endcontent-ref %}

{% content-ref url="assertnotvisible.md" %}
[assertnotvisible.md](assertnotvisible.md)
{% endcontent-ref %}
