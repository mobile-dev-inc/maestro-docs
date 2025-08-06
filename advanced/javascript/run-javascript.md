---
description: >-
  Run JavaScript in flows with runScript or evalScript, passing parameters and
  returning values. Part of Maestro testing tutorial.
---

# Run JavaScript

Maestro is not a JavaScript testing framework, but we recognize not everything can (or should) be written in YAML. That's why we have JavaScript support.

There are several ways to run JavaScript, depending on your needs.

{% hint style="info" %}
Right now, Rhino is the default JavaScript engine in Maestro, but we intend to make GraalJS the default soon and then deprecate and remove Rhino. We recommend everyone to opt-in to use GraalJS.

**Learn more about** [**GraalJS support**](graaljs-support.md).
{% endhint %}

## Inject

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

## Run file

If you want to run a JavaScript file you can use the runScript command:

{% content-ref url="../../api-reference/commands/runscript.md" %}
[runscript.md](../../api-reference/commands/runscript.md)
{% endcontent-ref %}

### Passing parameters

`runScript` accepts `env` parameters, in the same way as `runFlow` does (see [nested-flows.md](../nested-flows.md "mention")).

Passing a parameter:

```yaml
- runScript:
    file: script.js
    env:
       myParameter: Parameter
```

Reading a parameter in JavaScript:

```javascript
const readPassedParameter = myParameter;
console.log(readPassedParameter); // Outputs 'Parameter'
```

## Inline

For very simple computations (like the one above), creating a new file might be cumbersome. For this use case you can use the `evalScript` command:

{% content-ref url="../../api-reference/commands/evalscript.md" %}
[evalscript.md](../../api-reference/commands/evalscript.md)
{% endcontent-ref %}

## Inbuilt functions & properties

Whilst the JavaScript environment is limited, there are a few inbuilt things that can be used:

### object `maestro`

The `maestro` object contains the following properties:

| Field Name   | Value                                                                                                                                  |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `copiedText` | Results of the [copyTextFrom](../../api-reference/commands/copytextfrom.md) command. See [Access element text](access-element-text.md) |
| `platform`   | The platform the test is running on. Either `ios` or `android`                                                                         |

The `maestro.platform` value is useful for conditional logic that differs between Android and iOS. For example, you might want to handle location permission differently:

```yaml
- runScript: setPermissionsVars.js
- tapOn: "Enable Location"
- assertVisible: ${output.locationPermissionAlert}
- tapOn: ${output.locationPermissionButton}
```

{% code title="setPermissionsVars.js" %}
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
{% endcode %}

### function `relativePoint`

The `relativePoint` function converts decimal values to string percentages, which is the format that Maestro commands expect.

```yaml
- evalScript: ${output.specialPoint = relativePoint(0.13, 0.56)}
- tapOn:
    point: ${output.specialPoint} # Taps on the point '13%,56%'
```

### Others

The following inbuilt functions are documented in [Make HTTP requests](make-http-s-requests.md):

* http.request
* http.get
* http.post
* http.put
* http.delete
* json
