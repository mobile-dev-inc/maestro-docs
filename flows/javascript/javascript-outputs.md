---
description: >-
  Store JavaScript results in the global output object and use them in
  subsequent Flow commands.
hidden: true
---

# JavaScript outputs

While optional, it's common practice to execute JavaScript code within a flow to generate dynamic results that you can use in subsequent commands. By leveraging script execution, you can compute values, transform inputs, or perform logic, then expose the results via the shared `output` object for use elsewhere in the workflow.

### Output

The whole flow shares a single global `output` object in JavaScript that you can modify to include results of a flow:

```javascript
// myScript.js
output.result = 'Hello World'
```

You can later access it in the flow itself or in other scripts:

```yaml
- runScript: myScript.js
- inputText: ${output.result}
```

{% hint style="info" %}
In the preceding example, `result` is just an arbitrary name. It could be anything.
{% endhint %}

### Output namespaces

Since `output` field is global, several scripts might clash with each other. Consider this example:

```javascript
// mySecondScript.js
output.result = 'Bye World'
```

The following flow then prints `Bye World`, overriding the `Hello World` result from `myScript.js`.

```yaml
- runScript: myScript.js
- runScript: mySecondScript.js
- inputText: ${output.result}   # inputs 'Bye World'
```

To avoid such conflicts, consider using `namespaces` for your outputs:

```javascript
// myScript.js
output.myScript = {
    result: 'Hello World'
}
```

And, you run the Javaxcript file that results on a output:

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
