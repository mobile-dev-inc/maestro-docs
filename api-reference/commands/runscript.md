# runScript

For more information regarding JavaScript, please refer to the Javascript section:

{% content-ref url="../../advanced/javascript/" %}
[javascript](../../advanced/javascript/)
{% endcontent-ref %}

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

A script would typically perform some action and set an output value that could be accessed later. See [outputs.md](../../advanced/javascript/outputs.md "mention") for more information.

```javascript
var uppercaseName = MY_NAME.toUpperCase()

output.myFlow = uppercaseName   // returns 'JOHN'
```

{% hint style="info" %}
You can directly access `env` parameters from within JavaScript. See [parameters-and-constants.md](../../advanced/parameters-and-constants.md "mention") for more information.
{% endhint %}

#### Passing parameters

`runScript` accepts `env` parameters, in the same way as `runFlow` does (see [nested-flows.md](../../advanced/nested-flows.md "mention")).

```javascript
- runScript:
    file: script.js
    env:
       myParameter: 'Parameter'
```

#### Running conditionally

You can use conditionals to run a JavaScript file when some condition is true. For more information, please refer to the [conditionals](../../advanced/conditions.md) documentation.

#### Console logging&#x20;

Console logging is supported from the javascript files provided in `runScript` command. Logs from javascript are redirected to the console when using Maestro CLI.&#x20;

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
