---
description: Embed JavaScript directly in YAML flows using evalScript and runScript.
hidden: true
---

# JavaScript on Maestro flows

When using Javascript wtht Maestro, you can perform a series of commands and subcommands inside your flows. The main ones are listed below.

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

You can run a `.js` file when running the flow. This file should be called this way:

#### Runscript

The `runScript` command runs a provided JavaScript file.

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- runScript: myScript.js
- inputText: ${output.myFlow}
```

A script would typically perform some action and set an output value that could be accessed later. See [outputs](https://docs.maestro.dev/advanced/javascript/outputs) for more information.

```javascript
var uppercaseName = MY_NAME.toUpperCase()

output.myFlow = uppercaseName   // returns 'JOHN'
```

{% hint style="info" %}
You can directly access `env` parameters from within JavaScript. See ghe [Parameters & Constants ](https://docs.maestro.dev/advanced/parameters-and-constants)documentation for more information.
{% endhint %}

#### File paths

Paths can be relative or absolute. Use relative paths for cloud running. Relative paths are relative to the calling flow, not to the directory running the command.

In a directory structure like this:

```
├── flows
│   └── test.yaml
└── scripts
    └── uppercase.js
```

The flow `test.yaml` would look like this:

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- runScript: ../scripts/uppercase.js
```

#### Pass parameters

The `runScript` accepts `env` parameters, in the same way as `runFlow` does (see [https://docs.maestro.dev/advanced/nested-flows](https://docs.maestro.dev/advanced/nested-flows "mention")).

```javascript
- runScript:
    file: script.js
    env:
       myParameter: 'Parameter'
```

#### Console logging

Console logging is supported from the JavaScript files provided in `runScript` command. Logs from JavaScript are redirected to the console when using Maestro CLI.

![](https://2384395183-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fn5KVIOjVkVjYRyVWZ0yT%2Fuploads%2Fgit-blob-d27f45fb129d9b9c99ce59bff140c60aac3fc89d%2Fimage.png?alt=media)

{% hint style="warning" %}
Remember that when running in the cloud and requiring another file, you must specify a folder on the command line, not just the flow file. For example, use `maestro cloud myApp.apk ./myTestsFolder` so Maestro has the files required to run your tests. Otherwise, you'll receive a 'Failed to parse file' error.
{% endhint %}

### Inbuilt functions and properties

Whilst the JavaScript environment is limited, there are a few inbuilt things that can be used:

#### `maestro` object

The `maestro` object contains the following properties:

| **Field Name** | **Description**                                                                                                                                                                                                                                                           |
| :------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  `copiedText`  | <p>Contains the result of the <a href="https://docs.maestro.dev/api-reference/commands/copytextfrom"><code>copyTextFrom</code></a> command.<br>Access <a href="https://docs.maestro.dev/advanced/javascript/access-element-text">Access element text</a> for details.</p> |
|   `platform`   | Indicates the platform the test is running on. Possible values: `android` or `ios`.                                                                                                                                                                                       |

The `maestro.platform` value is useful for conditional logic that differs between Android and iOS. For example, you might want to handle location permission differently:

```yaml
- runScript: setPermissionsVars.js
- tapOn: "Enable Location"
- assertVisible: ${output.locationPermissionAlert}
- tapOn: ${output.locationPermissionButton}
```

The `setPermissionsVars.js` will look like this:&#x20;

```javascript
// setPermissionsVars.js
if (maestro.platform === 'ios') {
    output.locationPermissionAlert = "This app uses your location to show you information about your local environment"
    output.locationPermissionButton = "Allow"
}
if (maestro.platform === 'android') {
    output.locationPermissionAlert = "Allow access to this device's location?"
    output.locationPermissionButton = "While using the app"
}
```

#### `relativePoint` function

The `relativePoint` function converts decimal values to string percentages, which is the format that Maestro commands expect, you can call thi functons as shown below:

```yaml
- evalScript: ${output.specialPoint = relativePoint(0.13, 0.56)}
- tapOn:
    point: ${output.specialPoint} # Taps on the point '13%,56%'
```

{% hint style="info" %}
You can access oher commands and subcommands on the [Make HTTP requests](https://docs.maestro.dev/advanced/javascript/make-http-s-requests) documetation.
{% endhint %}
