# Run and debug JavaScript

This guide explains how to execute JavaScript within your Maestro Flows and how to use logging to debug your scripts.

### Execution Methods

Maestro provides three ways to run JavaScript, depending on the complexity of the logic you need to perform.

#### 1. In-line expressions

For simple logic or dynamic values, use the `${}` syntax directly inside existing Maestro commands. This is ideal for string concatenation or basic math.

```yaml
- launchApp
- inputText: ${'User_' + faker.name().firstName()} # Generates a dynamic username
- tapOn: ${maestro.platform === 'ios' ? 'Allow' : 'While using the app'} # Conditional logic
```

{% hint style="info" %}
Learn how to[ generate synthetic data](generate-synthetic-data.md) using JavaScript.
{% endhint %}

#### 2. The `evalScript` Command

Use [`evalScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/evalscript) for logic-only steps that don't directly interact with a UI element, such as setting a variable or performing a calculation.

YAML

```
- evalScript: ${output.timestamp = new Date().getTime()} # Store data for later use
- evalScript: ${console.log('Test execution started')} # Inline logging
```

#### 3. The `runScript` Command

For complex logic, reusable functions, or long scripts, use [`runScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/runscript) to execute an external `.js` file.

You can pass environment variables to your script using the `env` attribute, similar to how you pass parameters to subflows. First, you use `runScript` to define the JavaScript file and the variables that will be shared with it:

```yaml
- runScript:
    file: setupUser.js
    env:
       userRole: 'admin' # Pass a parameter to the script
```

The JavaScript file can read the environment variable and use to perform the necessary actions.

```javascript
// Access the passed parameter directly by its name
const role = userRole; 
console.log(`Setting up user with role: ${role}`);
```

### Logging and debugging

Maestro supports standard `console.log` statements to help you debug your scripts and track Flow execution.

When logging with JavaScript in Maestro you have two main points:

* Maestro's `console.log` does not support multiple arguments. Running `console.log('My variable is', variable)` will only output `My variable is`.
* To log variables alongside text, use template literals or string concatenation.

The following code snippt shows examples of concatenation and template literals:

```javascript
console.log('Value: ' + myVar)   // concatenation
console.log(`Value is ${myVar}`) // template literals
```

#### Logging with `evalScript` command <a href="#logging-with-evalscript-command" id="logging-with-evalscript-command"></a>

If you want to log something inline you can use [`evalScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/evalscript) to output it to the console without having to create a separate file:

```yaml
- evalScript: ${console.log('Hello from Javascript')}
```

#### Logging in external files

When using `runScript`, you can organize your logs within your JavaScript files just as you would in a standard development environment.

The following Flow runs the script, which will log the message.

{% tabs %}
{% tab title="Flow" %}
```yaml
- runScript:
    file: script.js
```
{% endtab %}

{% tab title="JavaScript file (script.js)" %}
```js
// script.js
const status = 'Success';
console.log(`Operation status: ${status}`); // Outputs 'Operation status: Success'
```
{% endtab %}
{% endtabs %}

### Next steps

Now that you already knows how to run and debug JavaScript code in Maestro Flows, access the following guides:

* [manage-data-and-states.md](manage-data-and-states.md "mention"):
* [generate-synthetic-data.md](generate-synthetic-data.md "mention"):&#x20;
* [make-http-requests.md](make-http-requests.md "mention"):

