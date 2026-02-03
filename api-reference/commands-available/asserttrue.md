# assertTrue

Asserts that a given expression evaluates to a truthy value. A value is [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) (in JavaScript terms) if it is not `false`, `0`, an empty string (`""`), `null`, `undefined`, or `NaN`.

### Syntax

You can use the shorthand approach, providing only the expression, or you can use the `condition` and `label`.

```yaml
- assertTrue: ${value}
# or
- assertTrue:
    condition: ${value}
    label: Variable 'value' is set
```

### Parameters

You can provide the expression directly or use the `condition` and `label` parameters for more complex assertions.

| Parameter   | Type       | Description                                                              |
| ----------- | ---------- | ------------------------------------------------------------------------ |
| `condition` | Expression | The expression to evaluate. The test passes if the expression is truthy. |
| `label`     | String     | An optional message to display when executing the evaluation.            |

### Usage examples

The following examples show how to use the `assertTrue` command.

#### Assert a JavaScript expression

This example uses `assertTrue` to verify that the text content of two separate views is identical. The `label` states the purpose of the assertion.

```yaml
- copyTextFrom: View A
- evalScript: ${output.viewA = maestro.copiedText}

- copyTextFrom: View B
- evalScript: ${output.viewB = maestro.copiedText}

- assertTrue:
    condition: ${output.viewA == output.viewB}
    label: View A and View B show the same text
```

#### Fail a test with a custom message

This example uses the `condition` and `label` parameters to intentionally fail a test and provide a descriptive reason.

```yaml
- assertTrue:
    condition: ${false}
    label: This will always fail
```

### Related commands

* [assertvisible.md](assertvisible.md "mention")
* [assertnotvisible.md](assertnotvisible.md "mention")
