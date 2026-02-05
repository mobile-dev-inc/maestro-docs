---
description: Assert that two values are equal in Maestro flows.
---

# assertEqual

Asserts that two values are equal after JavaScript evaluation:

```yaml
- assertEqual:
    value1: ${actualValue}
    value2: "expected"
```

This command compares `value1` and `value2` as strings after evaluating any JavaScript expressions. If the values are not equal, the assertion fails with a clear error message showing both values.

### Basic usage

Compare a variable to an expected value:

```yaml
- assertEqual:
    value1: ${output.username}
    value2: "john_doe"
```

Compare two JavaScript expressions:

```yaml
- assertEqual:
    value1: ${2 + 2}
    value2: ${8 - 4}
```

Compare text copied from the UI:

```yaml
- copyTextFrom: 
    id: "price-label"
- assertEqual:
    value1: ${maestro.copiedText}
    value2: "$19.99"
```

### With label and optional

Add a descriptive label or make the assertion optional:

```yaml
- assertEqual:
    value1: ${output.status}
    value2: "success"
    label: "Verify API returned success status"
    optional: true
```

### Use in conditions

`assertEqual` can be used in `runFlow` and `repeat` conditions:

```yaml
- runFlow:
    when:
      equal:
        value1: ${platform}
        value2: "ios"
    commands:
      - tapOn: "iOS-specific button"
```

```yaml
- repeat:
    while:
      equal:
        value1: ${output.loading}
        value2: "true"
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

{% content-ref url="assertnotequal.md" %}
[assertnotequal.md](assertnotequal.md)
{% endcontent-ref %}

{% content-ref url="asserttrue.md" %}
[asserttrue.md](asserttrue.md)
{% endcontent-ref %}

{% content-ref url="assertvisible.md" %}
[assertvisible.md](assertvisible.md)
{% endcontent-ref %}
