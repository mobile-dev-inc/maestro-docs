# repeat

A command to repeat a set commands until a condition is met.

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

Repeat set of commands until a condition is satisfied.

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

{% content-ref url="../../advanced/conditions.md" %}
[conditions.md](../../advanced/conditions.md)
{% endcontent-ref %}

{% hint style="info" %}
If you need to, you can specify both a count and a condition, for example repeating a set of commands whilst an element isn't visible, up to a maximum count of 10 times
{% endhint %}
