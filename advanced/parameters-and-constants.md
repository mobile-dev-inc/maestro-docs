---
description: >-
  Pass parameters and set environment variables in Maestro flows with env and
  reuse via ${}.
---

# Parameters & Constants

### External parameters

There might be cases where you don't want to store certain values in a test file itself (i.e. user name, password, etc.). To solve that, you can pass parameters to Maestro:

```
maestro test -e USERNAME=user@example.com -e PASSWORD=123 file.yaml
```

And then refer to them in your flow using `${name}` notation:

```yaml
appId: your.app.id
---
- launchApp
- inputText: ${USERNAME}
- tapOn: Next
- inputText: ${PASSWORD}
```

In a similar fashion, parameters can be passed to `maestro cloud` command:

```
maestro cloud -e USERNAME=user@example.com -e PASSWORD=123 app.apk file.yaml
```

### Inline parameters

Constants can be declared at the flow file level, above the `---` marker:

```yaml
appId: your.app.id
env:
    USERNAME: user@example.com
    PASSWORD: 123
---
- inputText: ${USERNAME}
- inputText: ${PASSWORD}
```

Alternatively, they can be passed to a `runFlow` command:

```yaml
appId: your.app.id
---
- runFlow:
    file: subflow.yaml
    env:
      USERNAME: user@example.com
      PASSWORD: 123
```

{% content-ref url="nested-flows.md" %}
[nested-flows.md](nested-flows.md)
{% endcontent-ref %}

{% hint style="info" %}
Constants defined in a nested flow override parameters with the same name in the parent flow.
{% endhint %}

### Accessing variables from the shell

Maestro will automatically read environment variables from the shell prefixed by `MAESTRO_` and make them available in your Flows, assuming the environment variable is not manually defined in the Flow or passed as an env parameter.&#x20;

```
export MAESTRO_FOO=bar
```

If you define the variable `MAESTRO_FOO` as above, you can simply refer to it in your Flows when running `maestro test` or `maestro cloud` like a normal environment variable:

```
- tapOn: ${MAESTRO_FOO}
```

### Parameters and JavaScript

All `env` parameters are defined as JavaScript variables under the hood and can be accessed from the JavaScript code.

{% content-ref url="javascript/" %}
[javascript](javascript/)
{% endcontent-ref %}
