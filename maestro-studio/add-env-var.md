# Environment variables on Maestro Studio

As part of the workspace for tests, you can set environment variables to work with. This is useful to save time when typing your email address or your password for a test. It also helps to avoid errors due to typos and helps you keep your data safe by not adding sensitive information to tests. This way, you can share the YAML file with other people.

## Add an environment

When you start using Maestro Studio, you have the default environment, called `None`. But, to better organize your tests, it's recommended to have environments and environment variables separated.

To add a new environment, follow these steps:

1. Open the Maestro Studio.
2. In Maestro Studio, click the gear icon.
3. On the dropdown menu, select **Environments** to open the **Environment Manager** window.

![Open the Environment options](/images/maestro-studio/environment.png)

4. In the **Environment Manager**, click the **+ Add Environment** button.

![Add an environment](/images/maestro-studio/add-env.png)

## Add environment variables

To add new variables to your workspace, follow these steps:

1. Open the Maestro Studio.
2. In Maestro Studio, click the gear icon.
3. On the dropdown menu, select **Environments** to open the **Environment Manager** window.

![Open the Environment options](/images/maestro-studio/environment.png)

4. In the **Environment Manager**, click the **+ Add Variable** button.

![Add an environment variable](/images/maestro-studio/add-var.png)

5. Add the variables as key-value pairs. For example, you can add the following variables:
    - **email**: `test@test.com`.
    - **password**: `12345678`.
6. Click the **Save** button.

Now you're ready to use your variables in your flows.

{% hint style="success" %}
You can have as many environments as you want, with as many environment variables as you want.
{% endhint %}

## Use environment variables on your flows

To use your variables in your flows, just reference them inside the YAML file as shown below:

```yaml
appId: https://docs.maestro.dev/
name: Test1
env:
  USERNAME: ${email}
  PASSWORD: ${password}
---
- launchApp:
    clearState: true
```

This uses the variables you have declared in your environment directly in your flows.