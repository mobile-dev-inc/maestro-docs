# assertTrue

Asserts whether given value is either true, non-empty, or _truthy_ ([in JavaScript terms](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)):

```yaml
- assertTrue: ${value}
```

This command is primarily designed to be used in combination with JavaScript
values. For example, you can assert that two views have the same text:

```yaml
- copyTextFrom: View A
- evalScript: ${output.viewA = maestro.copiedText}
- copyTextFrom: View B
- assertTrue: ${output.viewA == maestro.copiedText}
```

You can also use it to immediately fail the test:

```yaml
- assertTrue:
    condition: ${false}
    label: This will always fail
```


#### Related commands

{% content-ref url="assertvisible.md" %}
[assertvisible.md](assertvisible.md)
{% endcontent-ref %}

{% content-ref url="assertnotvisible.md" %}
[assertnotvisible.md](assertnotvisible.md)
{% endcontent-ref %}
