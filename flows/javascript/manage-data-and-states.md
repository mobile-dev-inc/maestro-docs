# Manage data and states

Sharing data between UI elements and JavaScript scripts is essential for creating dynamic, resilient tests. This guide covers how to use the global `output` object, manage namespaces, and capture UI text for use in your logic.

### The `output` object

Maestro provides a single, global JavaScript object called `output` that persists throughout the entire execution of a Flow. Any data assigned to this object in one script or expression is immediately accessible to all subsequent scripts and Maestro commands.

You can store strings, numbers, booleans, or complex objects within `output`.

You can access or add information to the `output` object using JavaScript notation. In the following example, the value `'Hello World'` is assigned to the `result` key (which is used as an arbitrary key, you could use wherever you want):

```javascript
// myScript.js
output.result = 'Hello World'
```

The Flow runs the `myScript.js` , which assined the value to the global object. After, the value is used to to input text in the text field using `inputText`:

```yaml
- runScript: myScript.js
- inputText: ${output.result}
```

### Output Namespacing

Because the `output` object is global, scripts can accidentally overwrite each other’s data if they use the same variable names. To prevent this, use namespaces, sub-objects named after your specific script or feature.

For example, instead of assigning variables directly to `output`, group them by context:

{% tabs %}
{% tab title="authScript.js" %}
```javascript
output.auth = {
    token: "abc-123",
    expiry: 3600
};
```
{% endtab %}

{% tab title="profileScript.js" %}
```javascript
output.profile = {
    username: "MaestroUser",
    role: "Admin"
};
```
{% endtab %}
{% endtabs %}

Then, you can access the data using the namespaced data:

```yaml
- inputText: ${output.auth.token}
- assertVisible: ${output.profile.username}
```

### The `maestro` Object

The `maestro` object is a built-in utility that provides information about the current test environment and captured UI data.

<table data-header-hidden><thead><tr><th width="185.6666259765625"></th><th></th></tr></thead><tbody><tr><td><strong>Property</strong></td><td><strong>Description</strong></td></tr><tr><td><code>maestro.copiedText</code></td><td>Contains the text retrieved by the most recent <a href="https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/copytextfrom"><code>copyTextFrom</code></a> command.</td></tr><tr><td><code>maestro.platform</code></td><td><p>Identifies the OS, either:</p><ul><li><code>ios</code> </li><li><code>android</code> </li><li><code>web</code></li></ul><p>It is useful for <a href="../flow-control-and-logic/conditions.md">conditional</a> cross-platform logic.</p></td></tr></tbody></table>

#### Capturing UI Text

To move text from your application into your JavaScript logic:&#x20;

1. First, use the [`copyTextFrom`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/copytextfrom) command to add the content to the `maestro.copiedText` object.
2. After, access the content and use in your JavaScript code using  `maestro.copiedText`.

The example copies the content from the `userName` element, and uses it to sear

```yaml
- copyTextFrom: 
    id: userName # Target the userName element
- inputText: ${'Hello ' + maestro.copiedText} # Sends the message using the userName
```

### Advanced: Shared Functions

The `output` object can also store functions, allowing you to define reusable logic (like API helpers) once and call them anywhere in your Flow.

`apiUtils.js`

```javascript
function generateToken(prefix) {
    return prefix + "_" + Math.random().toString(36);
}

output.utils = {
    generateToken: generateToken
};
```

Maestro Flow:

```yaml
- onFlowStart:
    - runScript: apiUtils.js
---
- evalScript: ${output.sessionToken = output.utils.generateToken('session')}
```

