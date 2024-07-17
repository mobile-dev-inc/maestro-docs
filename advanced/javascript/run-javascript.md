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

If you want to run a JavaScript file you can use the runScript command:

{% content-ref url="../../api-reference/commands/runscript.md" %}
[runscript.md](../../api-reference/commands/runscript.md)
{% endcontent-ref %}

#### Passing parameters

`runScript` accepts `env` parameters, in the same way as `runFlow` does (see [nested-flows.md](../nested-flows.md "mention")).

Passing a parameter:

```javascript
- runScript:
    file: script.js
    env:
       myParameter: 'Parameter'
```

Reading a parameter in Javascript:

```javascript
const readPassedParameter = myParameter;
```

### Inline

For very simple computations (like the one above), creating a new file might be cumbersome. For this use case you can use the `evalScript` command:

{% content-ref url="../../api-reference/commands/evalscript.md" %}
[evalscript.md](../../api-reference/commands/evalscript.md)
{% endcontent-ref %}
