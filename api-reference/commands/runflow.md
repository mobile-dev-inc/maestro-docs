# runFlow

If you'd like to avoid duplication of code or otherwise modularize your Flow files, you can use the `runFlow` command to run commands from another file.

### runFlow

Runs a flow from a specified file:

```yaml
- runFlow: anotherFlow.yaml
```

#### Example

Let's say you have a login sequence that you'd like to reuse across multiple flows. You can write the login commands in a separate file and run those steps from another Flow:

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

#### Arguments

`runFlow` command can accepts arguments that will be passed to subflow, the same way as with `-e` or `env` block in the flow itself (see [Parameters & Constants](../../advanced/parameters-and-constants.md)):

```yaml
- runFlow: 
    file: anotherFlow.yaml
    env:
      MY_PARAMETER: "123"
```

#### Inline flows

If you would like to use `runFlow` without extracting the commands into a separate flow file, you can run your commands inline like this:

```yaml
- runFlow:
    env:
      INNER_ENV: Inner Parameter
    commands:
      - inputText: ${INNER_ENV}
```



{% hint style="warning" %}
Remember that when using Robin and requiring another file, you must specify a folder on the command line not just the flow file, e.g. `maestro cloud myApp.apk ./myTestsFolder` else Robin won't have the files required to run your tests, and you'll receive a 'Failed to parse file' error.
{% endhint %}
