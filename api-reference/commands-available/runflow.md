# runFlow

The `runFlow` command executes a sequence of commands from another Flow file or from an inline definition. This command helps you modularize tests and reuse common sequences, such as a login process.

### Parameters

The `runFlow` command accepts the following parameters.

<table><thead><tr><th width="115.33331298828125">Parameter</th><th width="95.4444580078125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>file</code></td><td><code>string</code></td><td>The relative path to the Flow file to execute.</td></tr><tr><td><code>env</code></td><td><code>map</code></td><td>A map of key-value pairs to pass as environment variables to the subflow.</td></tr><tr><td><code>commands</code></td><td><code>list</code></td><td>A list of commands to execute inline. Use this instead of the <code>file</code> parameter for self-contained Flows.</td></tr></tbody></table>

### Usage examples

The following examples demonstrate how to use the `runFlow` command.

#### Run a separate Flow file

To reuse a common sequence of steps, define them in a separate file and call them with `runFlow`. For example, you can define a login sequence once and reuse it in multiple tests. The following **Login** Flow is defined in one file and reused in the other two Flows (**Profile** and **Settings**).

{% tabs %}
{% tab title="Login.yaml" %}
```yaml
appId: com.example.app
---
- launchApp
- tapOn: Username
- inputText: Test User
- tapOn: Password
- inputText: Test Password
- tapOn: Login
```
{% endtab %}

{% tab title="Profile.yaml" %}
```yaml
appId: com.example.app
---
- runFlow: Login.yaml # <-- Run commands from "Login.yaml"
- tapOn: Profile
- assertVisible: "Name: Test User"
```
{% endtab %}

{% tab title="Settings.yaml" %}
```yaml
appId: com.example.app
---
- runFlow: Login.yaml # <-- Run commands from "Login.yaml"
- tapOn: Settings
- assertVisible: "Switch to dark mode"
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Prefer using Flow files if the same flow will be reused across multiple tests. Otherwise, defining Flows files can make it harder to quickly understand what’s happening in your test.
{% endhint %}

#### Pass environment variables to a subflow

You can pass variables to the subflow using the `env` parameter. These variables are accessible within the subflow.

```yaml
- runFlow: 
    file: anotherFlow.yaml
    env:
      MY_PARAMETER: "123"
```

#### Run an inline Flow

To define a subflow directly within the `runFlow` command, use the `commands` parameter instead of `file`.

```yaml
- runFlow:
    env:
      INNER_ENV: Inner Parameter
    commands:
      - inputText: ${INNER_ENV}
```

{% hint style="success" %}
Inline subflows are primarily useful for [conditional](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/conditions) logic or small flows that don’t need a separate file.
{% endhint %}

### Cloud execution

When you run a test in Maestro Cloud that uses `runFlow` to call another file, you must specify the parent directory in the `maestro cloud` command. This ensures that Maestro uploads all necessary files. If you only specify the main Flow file, the command fails with a `Failed to parse file` error.

For example, if your files are in a `myTestsFolder` directory, use the following command:

```bash
maestro cloud myApp.apk ./myTestsFolder
```

### Related content

Learn how to define parameters and set environment variables in Maestro Flows by accessing the [Parameters](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters "mention") and [Constants](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/constants "mention") pages.
