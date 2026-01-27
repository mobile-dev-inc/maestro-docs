# runScript

The `runScript` command executes a specified JavaScript file. The script can access environment variables and set [output](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/javascript/javascript-outputs) values for subsequent commands in the flow.

### Parameters

The `runScript` command accepts either a string that specifies the file path or a map that contains the file path and environment variables.

<table><thead><tr><th width="124.5555419921875">Key</th><th>Description</th></tr></thead><tbody><tr><td><code>file</code></td><td>The path to the JavaScript file to execute. Paths can be absolute or relative to the flow file.</td></tr><tr><td><code>env</code></td><td><strong>(Optional)</strong> A map of key-value pairs to pass as environment variables to the script.</td></tr></tbody></table>

### Usage examples

The following examples demonstrate how to use the `runScript` command.

#### Basic execution

Use `runScript` with a file path to execute a script. The script can access predefined `env` variables from the flow and set `output` values for later use.

{% tabs %}
{% tab title="Flow file" %}
```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- runScript: myScript.js
- inputText: ${output.uppercaseName}
```
{% endtab %}

{% tab title="JavaScript file (myScript.js)" %}
```javascript
var uppercaseName = MY_NAME.toUpperCase()

output.uppercaseName = uppercaseName   // returns 'JOHN'
```
{% endtab %}
{% endtabs %}

In this example, the flow launches the app and then executes an external JavaScript file using `runScript`. The script reads the `MY_NAME` environment variable defined in the flow, converts it to uppercase, and stores the result in `output.uppercaseName`. That output value is then used in the next step to input the text `"JOHN"` into the app.

#### File paths

Paths can be relative or absolute.&#x20;

When running in the cloud, relative paths are required. Relative paths are resolved from the calling flow’s location, not from the directory where the command is executed.

Given the following directory structure:

```
├── flows
│   └── test.yaml
└── scripts
    └── uppercase.js
```

The `test.yaml` flow must use a relative path to reference `uppercase.js`:

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- runScript: ../scripts/uppercase.js
```

#### Passing parameters

To pass parameters directly to a script, use the expanded map syntax with the `env` key.

```yaml
- runScript:
    file: script.js
    env:
       myParameter: 'Parameter'
```

#### Console logging

`runScript` redirects any `console.log()` output from the JavaScript file to the Maestro CLI console.

<figure><img src="https://2384395183-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fn5KVIOjVkVjYRyVWZ0yT%2Fuploads%2Fgit-blob-d27f45fb129d9b9c99ce59bff140c60aac3fc89d%2Fimage.png?alt=media" alt="Console output from a JavaScript file."><figcaption></figcaption></figure>

### Cloud execution

When you run flows in Maestro Cloud, you must upload the directory that contains your flows and scripts, not just a single flow file. For example, use `maestro cloud --app-file myApp.apk --flows ./myTestsFolder`.

If you do not include the script files in the upload, the execution fails with a `Failed to parse file` error.

### Related content

* [JavaScript overview](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/javascript/javascript-overview): Start exploring how to use JavaScript in your tests.
* [JavaScript outputs](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/javascript/javascript-outputs): Learn how to store and consume JavaScript outputs in Maestro flows.
* [Parameters](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants): Learn how to define and use parameters in flows to make them reusable.
* [Constants](/broken/spaces/mS3lsb9jRwfRHqddeRXG/pages/DLtBiFLCJpsE4uxGnPNx): Learn how to define constant values and reuse them across your flows.
* [Nested flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/nested-flows): Learn how to compose flows by calling one flow from another.
* [Conditional execution](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/conditions): Learn how to control flow execution using conditions and branching logic.
