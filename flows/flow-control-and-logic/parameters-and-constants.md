# Parameters and constants

Maestro allows you to inject data into your Flows to make them dynamic and reusable. Instead of hardcoding values like usernames, passwords, or product IDs, you can use variables that are populated at runtime.

There are two main ways to define these variables:

* **Parameters**: Values passed externally (e.g., from the CLI or CI/CD pipeline).
* **Constants**: Values defined internally within the Flow (e.g., using the `env` key).

Both are accessed using the same `${VARIABLE_NAME}` syntax.

{% hint style="info" %}
#### **Case sensitivity**

Variable names are case-sensitive. `${APP_ID}` is different from `${App_ID}`.
{% endhint %}

### Parameters

Parameters are useful for passing sensitive data (like credentials) or environment-specific configurations (like URLs) that you don't want to commit to your repository.

#### Passing parameters via CLI

You can pass parameters to Maestro using the `-e` flag when running the `test` or `cloud` commands.

```bash
maestro test -e USERNAME=user@example.com -e PASSWORD=secret flow.yaml
```

{% hint style="info" %}
#### **Type safety**

Remember that CLI parameters are passed as strings. If you need a number or boolean, you may need to parse it in JavaScript (e.g., `parseInt(${COUNT})`).
{% endhint %}

In your Flow, you can access these values using the `${VARIABLE_NAME}` syntax. The following Flow uses the provided username and password to log in.

```yaml
appId: com.example.app
---
- launchApp
- tapOn: "Username"
- inputText: ${USERNAME}
- tapOn: "Password"
- inputText: ${PASSWORD}
```

#### Accessing shell variables

Maestro automatically reads shell environment variables prefixed with `MAESTRO_` and makes them available in your flows. This is convenient for CI/CD environments where secrets are often exposed as environment variables.

{% hint style="warning" %}
This feature works only with the Maestro CLI, not Maestro Studio.
{% endhint %}

```bash
export MAESTRO_API_KEY="12345"
maestro test flow.yaml
```

In this example, the API key exported in the shell is captured by the JavaScript script within the Flow.

```yaml
- runScript:
    script: |
       output.apiKey = "${MAESTRO_API_KEY}"
```

### Constants

Constants are variables defined directly within your Flow files. They are useful for defining test data, configuration flags, or reusable values that don't need to change between runs.

#### Defining inline constants

You can define constants at the top of your Flow file using the `env` key.

In this example, `DEFAULT_TIMEOUT` and `IS_DEBUG` are set as constants for the entire Flow file.

```yaml
appId: com.example.app
env:
    DEFAULT_TIMEOUT: 5000
    IS_DEBUG: true
---
- launchApp
```

#### Passing arguments to subflows

When using nested Flows, you can pass arguments to reuse the same subflow with different data. Variables defined in `env` are available only to that specific subflow execution.

In the following example, the `login.yaml` subflow is executed with the `USER_ROLE` constant set to `admin`.

```yaml
- runFlow:
    file: subflows/login.yaml
    env:
        USER_ROLE: "admin"
```

{% hint style="info" %}
#### **Priority**

Constants defined in a subflow (either in the `env` header or the `runFlow` command) override parameters with the same name from the parent flow.
{% endhint %}

### Setting default values

You can use JavaScript syntax to provide default values for parameters. This is used for preventing crashes if a parameter is not provided.

In this example, `${USERNAME}` will use the provided value if it exists, otherwise, it defaults to `"guest"`.

```yaml
- inputText: ${USERNAME || "guest"}
```

This technique is particularly powerful in subflows, allowing them to be run standalone (using defaults) or as part of a larger suite (using passed parameters).

```yaml
# subflows/login.yaml
appId: com.example.app
env:
    # Use the passed value, or default to a test account
    USER_ID: ${USER_ID || "test_user_1"}
---
- tapOn: "User ID"
- inputText: ${USER_ID}
```

### Built-in parameters

Maestro provides a set of built-in parameters that are available in all flows.

<table><thead><tr><th width="201.75">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>MAESTRO_FILENAME</code></td><td>The filename of the current flow (e.g., <code>login.yaml</code>).</td></tr></tbody></table>

### Next steps

To continue learning how to create Flows, check the following pages:

* [nested-flows.md](nested-flows.md "mention"): Learn more about using `runFlow` to pass environment variables.
* [Maestro CLI overview](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/ "mention") : Explore more options for the `-e` flag.
* [javascript-overview.md](../javascript/javascript-overview.md "mention"): Learn how to manipulate parameters using JavaScript logic.
