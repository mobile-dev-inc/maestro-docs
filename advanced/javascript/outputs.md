---
description: >-
  Store results in output object and use namespaces to share data in Maestro
  flows without conflicts.
---

# Outputs

Though entirely optional, normally one would run a JavaScript code in order to produce a result to be used with other commands.

### output

The whole flow shares a single global `output` JavaScript object that can be modified to include results of a flow:

```javascript
// myScript.js
output.result = 'Hello World'
```

Where it can later be accessed either in the flow itself or in other scripts:

```yaml
- runScript: myScript.js
- inputText: ${output.result}
```

Note that in the example above, `result` is just an arbitrary name. It could be anything.

### Output Namespaces

Since `output` field is **global,** several scripts might clash with each other. Consider this example:

```javascript
// mySecondScript.js
output.result = 'Bye World'
```

The following flow will then print `Bye World`, overriding `Hello World` result from `myScript.js`

```yaml
- runScript: myScript.js
- runScript: mySecondScript.js
- inputText: ${output.result}   # inputs 'Bye World'
```

To avoid such conflicts, consider using _namespaces_ for your outputs:

```javascript
// myScript.js
output.myScript = {
    result: 'Hello World'
}
```

```javascript
// mySecondScript.js
output.mySecondScript = {
    result: 'Bye World'
}
```

Where a flow can then be explicit about which output it wants to use:

```yaml
- runScript: myScript.js
- runScript: mySecondScript.js
- inputText: ${output.myScript.result}   # inputs 'Hello World'
- inputText: ${output.mySecondScript.result}   # inputs 'Bye World'
```

{% hint style="info" %}
Note that you have full control over how to structure the outputs and are free to keep them as sophisticated or simple as you want. By the end of the day, `output` is just a JavaScript object.
{% endhint %}
