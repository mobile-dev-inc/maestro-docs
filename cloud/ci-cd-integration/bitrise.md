---
description: >-
  Native Bitrise integration for Maestro Cloud. Set API Key, Project ID, and app
  binary path to trigger tests automatically.
---

# Bitrise

Maestro Cloud provides a native integration step for Bitrise, allowing you to trigger cloud tests with minimal configuration.

{% hint style="info" %}
**Maestro Cloud Plan required.**&#x20;

Bitrise integration is available on the [Maestro Cloud Plan](https://signin.maestro.dev/sign-up).
{% endhint %}

### Setting up Bitrise

Setting up Maestro Cloud in your Bitrise workflow is straightforward. Here’s how you can get it up and running:

1. First, head over to the [Maestro Dashboard](https://app.maestro.dev/) to get your **API Key** and **Project ID**.
2. In Bitrise, save your API Key as a secret variable (for example, `CLOUD_API_KEY`).

{% hint style="info" %}
Avoid using the `MAESTRO_` prefix for your secret names unless you specifically want them passed into the test run as environment variables.

Any variable prefixed with `MAESTRO_` will be [added as environment variable](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants) for your run.
{% endhint %}

3. Open the **Workflow Editor** and search for "Maestro" in the Bitrise step library. Add the step after your application binary build step.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

4. **Configure the Step**:
   * **API Key**: Enter your secret variable (e.g., `CLOUD_API_KEY`).
   * **Project ID**: Enter your Maestro Project ID.
   * **Build Path**: Provide the path to your built `.apk` or `.app` binary.

{% hint style="info" %}
Visit the [Maestro Step in the Bitrise catalog](https://bitrise.io/integrations/steps/maestro-cloud-upload) to see the full list of available step options.
{% endhint %}

5. **Workspace Validation**: Ensure that the **Flow Workspace** path matches your repository’s directory structure.

Once configured, Bitrise automatically triggers your Maestro tests in the cloud as part of your pipeline.

#### Device configuration

To target a specific OS version or device model, use the `device_os` and `device_model` inputs. Both inputs accept iOS and Android values.

```yaml
- maestro-cloud-upload@1:
    inputs:
    - api_key: $CLOUD_API_KEY
    - project_id: $MAESTRO_PROJECT_ID
    - app_file: $BITRISE_APK_PATH
    - device_os: android-34
    - device_model: pixel_6
```

| Input          | Description                                                                              | Example                    |
| -------------- | ---------------------------------------------------------------------------------------- | -------------------------- |
| `device_os`    | OS version to run against. Run `maestro list-cloud-devices` to see all supported values. | `iOS-26-2`, `android-34`     |
| `device_model` | Device model to run against. Run `maestro list-cloud-devices` to see all supported values. | `iPhone-17-Pro`, `pixel_6` |

{% hint style="warning" %}
The `android_api_level` input is **deprecated** in favor of `device_os`. Existing workflows that set `android_api_level` continue to work but emit a deprecation warning. Migrate to `device_os` (e.g. `device_os: android-34`) when convenient.
{% endhint %}

#### Next steps

Now that your CI pipeline is connected, consider optimizing your cloud runs:

* Set up notifications via [Slack](../notifications/set-slack-notification.md), [email](../notifications/set-email-notification.md), or [webhooks](../notifications/configure-webhooks.md) to stay informed about build and test results.
* [Configure the operating system](../environment-configuration/configure-the-os.md) for your runs to match your application and dependency requirements.
* Define [locales and time zones](../environment-configuration/app-locales-and-device-timezones.md) to ensure consistent behavior across environments and regions.
* Explore all the [subcommand options for `claud`.](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options#cloud)
