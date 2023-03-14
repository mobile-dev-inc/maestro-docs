# Run JavaScript

There are several ways to run JavaScript, depending on your needs.

### Inject

Everything within `${}` blocks is evaluated as JavaScript, allowing you to insert dynamically computed values into any other Maestro command.

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- inputText: ${1 + 1}               # Inputs '2'
- inputText: ${'Hello ' + MY_NAME}  # Inputs 'Hello John'
- tapOn: ${MY_NAME}                 # Taps on element with text 'John'
```

### Run file

`runScript` command runs a provided JavaScript file.

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- runScript: myScript.js
- inputText: ${output.myFlow}
```

A script would typically perform some action and set an output value that could be accessed later. See [outputs.md](outputs.md "mention") for more information.

```javascript
var uppercaseName = MY_NAME.toUpperCase()

output.myFlow = uppercaseName   // returns 'JOHN'
```

{% hint style="info" %}
You can directly access `env` parameters from within JavaScript. See [parameters-and-constants.md](../parameters-and-constants.md "mention") for more information.
{% endhint %}

#### Passing parameters

`runScript` accepts `env` parameters, in the same way as `runFlow` does (see [nested-flows.md](../nested-flows.md "mention"))

```javascript
- runScript:
    file: script.js
    env:
       myParameter: 'Parameter'
```

### Inline

For very simple computations (like the one above), creating a new file might be cumbersome. `evalScript` allows you to specify JavaScript directly in your Maestro flow.

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- evalScript: ${output.myFlow = MY_NAME.toUpperCase()}
- inputText: ${output.myFlow}
```
