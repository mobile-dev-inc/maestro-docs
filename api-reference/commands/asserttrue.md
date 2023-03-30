# assertTrue

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
