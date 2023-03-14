# Conditions

{% hint style="warning" %}
By design, Maestro discourages the usage of conditional statements unless absolutely necessary as they could easily ramp up the complexity of your tests.
{% endhint %}

### runFlow conditionally

```yaml
- runFlow:
    when:
      visible: Some Text
    file: {reference to another yaml file}
```

{% content-ref url="nested-flows.md" %}
[nested-flows.md](nested-flows.md)
{% endcontent-ref %}

### Conditions

Supported conditions include:

<pre class="language-yaml"><code class="lang-yaml"><strong>visible: { Element matcher }        # True if matching element is visible
</strong>notVisible: { Element matcher }     # True if matching element is not present
true: { Value }                     # True if given value is true or not empty
</code></pre>

### JavaScript

Usage of JavaScript conditions is possible via `true` condition:

```yaml
- runFlow:
    when:
      true: ${MY_PARAMETER == 'Something'}
    file: subflow.yaml
```

{% content-ref url="javascript/" %}
[javascript](javascript/)
{% endcontent-ref %}
