# evalScript

The `evalScript` command executes a single line of JavaScript directly within a Maestro flow. This is useful for performing simple computations or data manipulations without creating a separate JavaScript file.

The command accepts a single string argument representing the JavaScript expression to evaluate.

### Syntax&#x20;

To use the `evalScript` command, you need to provide the single-line JavaScript expression to evaluate. The result can be assigned to the `output` scope for use in subsequent steps:

```yaml
- evalScript: ${output.myVar = myExpression}
```

### Usage examples

The following example uses `evalScript` to convert an environment variable to uppercase and stores the result in `output.uppercaseName`.

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- evalScript: ${output.uppercaseName = MY_NAME.toUpperCase()}
- inputText: ${output.uppercaseName}
```

### Related content

Access the [JavaScript guides](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/javascript/javascript-overview) to learn how to use JavaScript when creating Flows.
