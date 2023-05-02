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

#### Related commands

{% content-ref url="assertvisible.md" %}
[assertvisible.md](assertvisible.md)
{% endcontent-ref %}

{% content-ref url="assertnotvisible.md" %}
[assertnotvisible.md](assertnotvisible.md)
{% endcontent-ref %}
