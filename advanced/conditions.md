---
description: >-
  Use conditions in Maestro flows to run commands based on visibility, platform,
  or JavaScript expressions.
---

# Conditions

{% hint style="warning" %}
By design, Maestro discourages the usage of conditional statements unless absolutely necessary as they could easily ramp up the complexity of your tests.
{% endhint %}

### runFlow conditionally

```yaml
- runFlow:
    when:
      visible: 'Some Text'
    file: folder/some-flow.yaml
```

{% content-ref url="nested-flows.md" %}
[nested-flows.md](nested-flows.md)
{% endcontent-ref %}

Or, if you don't wish to extract your commands into a separate flow file, you can run the commands inline like this:

```yaml
- runFlow:
    when:
      visible: 'Some Text'
    commands:
        - tapOn: 'Some Text'
```

{% content-ref url="../api-reference/commands/runflow.md" %}
[runflow.md](../api-reference/commands/runflow.md)
{% endcontent-ref %}

### runScript conditionally

```yaml
- runScript:
    when:
      visible: 'Some Text'
    file: some-script.js
```

{% content-ref url="../api-reference/commands/runscript.md" %}
[runscript.md](../api-reference/commands/runscript.md)
{% endcontent-ref %}

### Multiple conditions

```yaml
- runFlow:
    when:
      visible: 'Some Text'
      platform: iOS
    file: folder/some-flow.yaml
```

Note that multiple conditions are applied as AND conditions.

### Conditions

Supported conditions include:

<pre class="language-yaml"><code class="lang-yaml"><strong>visible: { Element matcher }        # True if matching element is visible
</strong>notVisible: { Element matcher }     # True if matching element is not present
true: { Value }                     # True if given value is true or not empty
platform: { Platform }              # True if current platform is given platform (Android|iOS|Web)
equal: { value1, value2 }           # True if value1 equals value2
notEqual: { value1, value2 }        # True if value1 does not equal value2
</code></pre>

All of the normal element matchers are supported, e.g.

```yaml
- runFlow:
    when:
      visible:
        id: 'someId'
        text: 'Some Text'
        below:
          text: 'Some Other Text'
        childOf:
          id: 'someParentId'
          text: 'Some Parent Text'
        index: 2
    file: folder/some-flow.yaml
```

{% content-ref url="../api-reference/selectors.md" %}
[selectors.md](../api-reference/selectors.md)
{% endcontent-ref %}

### JavaScript

Usage of JavaScript conditions is possible via `true` condition:

```yaml
- runFlow:
    when:
      true: ${MY_PARAMETER == 'Something'}
    file: subflow.yaml
```

It's also possible to do platform detection in JavaScript:

```yaml
- runFlow:
    when:
      true: ${maestro.platform == 'android'}
    file: subflow.yaml
```

```javascript
if (maestro.platform == 'android'){
    output.searchTerm = 'robots'
}
if (maestro.platform == 'ios'){
    output.searchTerm = 'apples'
}
if (maestro.platform == 'web'){
    output.searchTerm = 'spiders'
}
```

{% content-ref url="javascript/" %}
[javascript](javascript/)
{% endcontent-ref %}
