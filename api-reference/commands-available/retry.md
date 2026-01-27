# retry

The `retry` command executes a set of commands repeatedly until they succeed or the maximum number of retries is reached. Use this command to handle intermittent or unpredictable behavior in your application.

### Parameters

The `retry` command accepts the following parameters:

<table><thead><tr><th width="132">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>maxRetries</code></td><td><strong>Optional.</strong> Specifies the number of times to retry the commands. The value must be between <code>0</code> and <code>3</code>. Defaults to <code>1</code>.</td></tr><tr><td><code>commands</code></td><td>A list of commands to execute. You must provide either <code>commands</code> or <code>file</code>.</td></tr><tr><td><code>file</code></td><td>The path to a file containing a flow to execute. You must provide either <code>file</code> or <code>commands</code>.</td></tr></tbody></table>

### Usage examples

The following example retries tapping a button up to three times. If the process is successful on the second attempt, the test will proceed to the next step, considering this one successful.

```yaml
- retry:
    maxRetries: 3
    commands:
      - tapOn:
          id: 'button-that-might-not-be-here-yet'
```
