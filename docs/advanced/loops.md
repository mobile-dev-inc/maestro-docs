# Loops

### Repeat

#### Repeat N times

Repeats set of commands N times

```yaml
- repeat:
    times: 3
    commands:
      - tapOn: Button
      - scroll
```

#### Repeat-while

Repeat set of commands until a condition satisfies.

```yaml
- repeat:
    while:
      notVisible: "ValueX"
    commands:
      - tapOn: Button
```

A condition can also be a JavaScript expression:

```yaml
- evalScript: ${output.counter = 0}
- repeat:
    while:
      true: ${output.counter < 3}
    commands:
      - tapOn: Button
      - evalScript: ${output.counter = output.counter + 1}
```

To learn more about conditions, see the following section:

{% content-ref url="conditions.md" %}
[conditions.md](conditions.md)
{% endcontent-ref %}

To learn more about JavaScript support refer to the following page:

{% content-ref url="javascript/" %}
[javascript](javascript/)
{% endcontent-ref %}
