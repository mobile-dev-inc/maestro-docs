---
description: >-
  Share data between scripts using the global output object, namespaces, and the
  maestro.copiedText property.
---

# Manage data and states

Sharing data between UI elements and JavaScript scripts is essential for creating dynamic, resilient tests. This guide covers how to use the global `output` object, manage namespaces, and capture UI text for use in your logic.

### The `output` object

Maestro provides a single, global JavaScript object called `output` that persists throughout the entire execution of a Flow. Any data assigned to this object in one script or expression is immediately accessible to all subsequent scripts and Maestro commands.

You can store strings, numbers, booleans, or complex objects within `output`.

You can store strings, numbers, booleans, or complex objects within `output`. You can access or add information to the `output` object using standard JavaScript notation. In the following example, the value `'Hello World'` is assigned to `result` (an arbitrary key name):

```javascript
// myScript.js
output.result = 'Hello World'
```

Once the Flow runs `myScript.js`, the value is assigned to the global object. You can then use that value in subsequent commands, such as `inputText`:

```yaml
- runScript: myScript.js
- inputText: ${output.result}
```

### Output Namespacing

Because the `output` object is global, scripts can accidentally overwrite each other’s data if they use the same variable names. To prevent this, use namespaces, sub-objects named after your specific script or feature.

Because the `output` object is global, different scripts can accidentally overwrite each other’s data if they use the same variable names. To prevent this, use namespaces (sub-objects named after your specific script or feature).

For example, instead of assigning variables directly to the root of `output`, group them by context:

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

You can then access this data using namespaced notation:

```yaml
- inputText: ${output.auth.token}
- assertVisible: ${output.profile.username}
```

### Shared Functions

The `output` object can store functions as well as data. This is a powerful pattern for defining reusable logic, such as API helpers or complex string formatters, at the start of a Flow so they can be called from any subsequent script.

In this example, we define a token generation function in `apiUtils.js` and make it globally available via the `output.utils` namespace:

```javascript
// apiUtils.js
function generateToken(prefix) {
    return prefix + "_" + Math.random().toString(36);
}

output.utils = {
    generateToken: generateToken
};
```

By loading the script in `onFlowStart`, the `generateToken` function becomes a reusable utility for the rest of the test execution:

```yaml
- onFlowStart:
    - runScript: apiUtils.js
---
# Call the shared function to generate a new session token
- evalScript: ${output.sessionToken = output.utils.generateToken('session')}
```

### The `maestro` Object

The `maestro` object is a built-in utility that provides information about the current test environment and captured UI data.

<table data-header-hidden><thead><tr><th width="185.6666259765625"></th><th></th></tr></thead><tbody><tr><td><strong>Property</strong></td><td><strong>Description</strong></td></tr><tr><td><code>maestro.copiedText</code></td><td>Contains the text retrieved by the most recent <a href="https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/copytextfrom"><code>copyTextFrom</code></a> command.</td></tr><tr><td><code>maestro.platform</code></td><td><p>Identifies the OS:</p><ul><li><code>ios</code> </li><li><code>android</code> </li><li><code>web</code></li></ul><p>This is useful for <a href="../flow-control-and-logic/conditions.md">conditional</a> cross-platform logic.</p></td></tr></tbody></table>

#### Capturing UI Text

To move text from your application into your JavaScript logic:&#x20;

1. Use the [`copyTextFrom`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/copytextfrom) command to store the content in the `maestro.copiedText` variable.
2. Access that content in your JavaScript code or Maestro commands using `maestro.copiedText`.

The following example copies content from a `userName` element and uses it to send a dynamic message:

```yaml
- copyTextFrom: 
    id: userName # Target the userName element
- inputText: ${'Hello ' + maestro.copiedText} # Greets the user using the captured name
```

### Next steps

Now that you already knows how to manage data when using JavaScript in Maestro Flows, access the following guides:

* [generate-synthetic-data.md](generate-synthetic-data.md "mention"): Use `faker` to create dynamic test data.
* [make-http-requests.md](make-http-requests.md "mention"): Use the built-in HTTP client for API interactions.
