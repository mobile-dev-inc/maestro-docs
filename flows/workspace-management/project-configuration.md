# Project configuration

The `config.yaml` file acts as the central "brain" of your Maestro workspace. While it is optional, it becomes essential when your project grows, allowing you to define global rules for your test suite, manage environment variables, and configure platform-specific behaviors.

### When do I need a config file?

If you are just running a single Flow file locally, you don't need a configuration. You should create a `config.yaml` if:

* You have a deep directory structure and need to define test discovery.
* You need to handle environment variables across multiple Flows.
* You want to disable system animations to reduce flakiness.

### Setting up your configuration

{% hint style="info" %}
#### Default Behavior & Hierarchy

If no `--config` flag is provided, Maestro will look for a file named `config.yaml` in the directory where you execute the command. If it doesn't find one, it will run with default settings.
{% endhint %}

{% stepper %}
{% step %}
### Create the configuration file

You can place your configuration file anywhere in your repository. While some teams prefer a `.maestro/` folder, you can simply place `config.yaml` at the root of your project for easier access.

{% hint style="info" %}
Ensure the file is named exactly `config.yaml`.
{% endhint %}
{% endstep %}

{% step %}
#### Define the application ID

The `appId` tells the Maestro engine which process to pilot. This is the only mandatory field for suite-wide testing.

```yaml
# config.yaml
appId: com.example.app
```

The `appId` targets different identifiers based on the platform:

* **iOS**: The Bundle ID (e.g., `com.company.appname`).
* **Android**: The Package Name (e.g., `com.company.appname`).
* **Web**: The base URL (e.g., `https://maestro.mobile.dev/`).
{% endstep %}

{% step %}
### Set the global environment variables

Use the `env` block to define data that changes across environments (staging vs. production, for example). This allows you to reference them in any Flow using the `${VARIABLE_NAME}` syntax without hardcoding secrets.

```yaml
# config.yaml
appId: com.example.app
env:
    USERNAME: "test_user_01"
    API_URL: "https://staging.api.com"
```

{% hint style="info" %}
If you are using Maestro Studio, it provides an interface for managing [environment variables](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/environment-variables).
{% endhint %}
{% endstep %}

{% step %}
### Configure the platform behavior

To ensure your tests are stable and flake-free, you can configure platform-specific behaviors. A common best practice is to disable system animations to prevent timing issues.

```yaml
# .maestro/config.yaml
platform:
  ios:
    disableAnimations: true           # Enables "Reduce Motion" on the simulator
    snapshotKeyHonorModalViews: false # Includes background elements in the hierarchy
  android:
    disableAnimations: true           # Disables system window and transition animations
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
&#x20;If you need a list of all configurations available to configure your test suite, access the [Workspace configuration](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/workspace-configuration "mention") reference.
{% endhint %}

### Working with multiple configs

While `config.yaml` is the default, you can create multiple configuration files for different scenarios (e.g., `smoke-config.yaml` or `ci-config.yaml`). To run a test suite with a specific configuration, use the `--config` flag when running the tests with the Maestro CLI:

```bash
maestro test --config .maestro/ci-config.yaml tests/
```

### Next steps

If you need a full list of every available key and configuration available, access the  [Workspace configuration](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/workspace-configuration "mention") reference page.

If you need to organize your tests, learn how to use the `flows` key in your config to manage Test Discovery & Tags.



