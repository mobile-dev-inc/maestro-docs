---
description: >-
  Run Maestro Cloud tests from Appcircle using the built-in Maestro Cloud Upload
  workflow step, or a Custom Script step with the Maestro CLI.
---

# Appcircle

[Appcircle](https://appcircle.io) is a mobile CI/CD platform, available as a cloud service or self-hosted. It provides a built-in **Maestro Cloud Upload** workflow step that installs the Maestro CLI, uploads your app binary and Flows, and runs them on Maestro Cloud as part of your build.

{% hint style="info" %}
**Maestro Cloud Plan required.**

Appcircle integration is available on the [Maestro Cloud Plan](https://signin.maestro.dev/sign-up).
{% endhint %}

{% stepper %}
{% step %}
### Save your API key and Project ID

Store your Maestro credentials as secret environment variables in Appcircle.

{% hint style="info" %}
#### API key and Project ID

You can find your API key and Project ID in the [Maestro Dashboard](https://app.maestro.dev/). The Project ID is listed in the Dashboard **Settings** for each project.
{% endhint %}

1. In Appcircle, open the **Build** module and select **Environment Variables**.
2. Create a variable group (for example, `MAESTRO_CLOUD`) using **Add Variable Group**.
3. Add the following variables and mark them as secret using the lock icon:
   * `AC_MAESTRO_API_KEY`: Your Maestro Cloud API key.
   * `AC_MAESTRO_PROJECT_ID`: Your Maestro Project ID.
4. Open your build profile's **Configuration**, go to the **Env. Variables** tab, and select the group you created.

{% hint style="info" %}
Avoid using the `MAESTRO_` prefix for your secret names unless you specifically want them passed into the test run as environment variables.

Any variable prefixed with `MAESTRO_` will be [added as environment variable](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants) for your run.
{% endhint %}
{% endstep %}

{% step %}
### Organize your Flows

Add your Flow files to a single directory in your repository. The Appcircle step looks for a `.maestro` directory in the repository root by default.

```
<root>
├── .maestro/
│   ├── subflows/
│   │   └── LoginSubflow.yaml
│   ├── Login.yaml
│   └── Search.yaml
```

Files in subdirectories (like `subflows/`) are not executed as top-level tests, but can be called by other Flows using the `runFlow` command.
{% endstep %}

{% step %}
### Build your app for the cloud

Add a build step that produces a binary Maestro Cloud can run. See [build-your-app-for-the-cloud.md](../build-your-app-for-the-cloud.md "mention") for the full requirements.

| Platform | Appcircle build step                                                                                                                         | Output variable          |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Android  | [Android Build](https://docs.appcircle.io/workflows/android-specific-workflow-steps/android-build) (ARM-compatible or multi-architecture APK) | `$AC_APK_PATH`           |
| iOS      | [Xcodebuild for iOS Simulator](https://docs.appcircle.io/workflows/ios-specific-workflow-steps/xcodebuild-for-ios-simulator)                 | `$AC_SIMULATOR_APP_PATH` |

{% hint style="warning" %}
Maestro Cloud needs an iOS **Simulator** build (`.app`). An `.ipa` built for physical devices will not run on Maestro Cloud.
{% endhint %}
{% endstep %}

{% step %}
### Add the Maestro Cloud Upload step

1. Open your build profile, go to **Workflows**, and click **Manage Workflow**.
2. Search for **Maestro Cloud Upload** and add it after your build step.
3. Configure the step inputs:
   * **API key**: `$AC_MAESTRO_API_KEY`
   * **App File**: `$AC_APK_PATH` for Android, or `$AC_SIMULATOR_APP_PATH` for iOS.
   * **Flow file or directory**: The directory that contains your Flows (default `.maestro`).
4. Click **Save** and start a build.

The step waits for the cloud run to finish and fails the build if any Flow fails, unless **Async Mode** is enabled. A link to the upload in the Maestro Console is printed in the build log.

| Input                      | Description                                                                                                            |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Upload Name                | Custom name for the upload. Defaults to the commit message.                                                            |
| Async Mode                 | Exit right after the upload, without waiting for the results.                                                          |
| Environment variables      | Variables passed to your Flows, one `KEY=value` per line.                                                              |
| Include tags, Exclude tags | Run only, or skip, Flows with the given comma-separated tags.                                                          |
| Export test report (JUnit) | Save a JUnit report of the run to `$AC_OUTPUT_DIR/maestro/maestro_report.xml`, so it can be exported with the build artifacts. |
| Mapping File               | Proguard mapping file (Android) or `.dSYM` file (iOS).                                                                 |
| Maestro CLI version        | Maestro CLI version to install. Defaults to the latest version.                                                        |

For the full list of inputs, see the [Maestro Cloud Upload step documentation](https://docs.appcircle.io/workflows/common-workflow-steps/maestro-cloud-upload) on the Appcircle website.

{% hint style="warning" %}
**Project selection**

The **Maestro Cloud Upload** step doesn't have a Project ID input. It works when your Maestro account has a **single project**, which the CLI selects automatically. If your account has more than one project, or you need to choose a device model and OS version with `--device-os` and `--device-model`, use the **Custom Script** option below.
{% endhint %}
{% endstep %}
{% endstepper %}

### Run the Maestro CLI from a Custom Script step

For full control over the `maestro cloud` options, add a [Custom Script](https://docs.appcircle.io/workflows/common-workflow-steps/custom-script) step after your build step, set **Execute with** to `bash`, and run the Maestro CLI directly:

{% tabs %}
{% tab title="Android" %}
```bash
set -e

curl -Ls "https://get.maestro.mobile.dev" | bash
export PATH="$PATH":"$HOME/.maestro/bin"

cd "$AC_REPOSITORY_DIR"

maestro cloud \
  --api-key "$AC_MAESTRO_API_KEY" \
  --project-id "$AC_MAESTRO_PROJECT_ID" \
  --app-file "$AC_APK_PATH" \
  --flows .maestro \
  --branch "$AC_GIT_BRANCH" \
  --device-os android-34 \
  --device-model pixel_6
```
{% endtab %}

{% tab title="iOS" %}
```bash
set -e

curl -Ls "https://get.maestro.mobile.dev" | bash
export PATH="$PATH":"$HOME/.maestro/bin"

cd "$AC_REPOSITORY_DIR"

maestro cloud \
  --api-key "$AC_MAESTRO_API_KEY" \
  --project-id "$AC_MAESTRO_PROJECT_ID" \
  --app-file "$AC_SIMULATOR_APP_PATH" \
  --flows .maestro \
  --branch "$AC_GIT_BRANCH" \
  --device-os iOS-26-2 \
  --device-model iPhone-17-Pro
```
{% endtab %}
{% endtabs %}

Run `maestro list-cloud-devices` to see all supported `--device-os` and `--device-model` values. `maestro cloud` exits with `1` if any Flow fails, which marks the Appcircle build as failed.

For a complete list of options, see the [`cloud` subcommand options](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options#cloud) in the Maestro CLI documentation.

#### Next steps

Now that your CI pipeline is connected, consider optimizing your cloud runs:

* Set up notifications via [Slack](../notifications/set-slack-notification.md), [email](../notifications/set-email-notification.md), or [webhooks](../notifications/configure-webhooks.md) to stay informed about build and test results.
* [Configure the operating system](../environment-configuration/configure-the-os.md) for your runs to match your application and dependency requirements.
* Define [locales and time zones](../environment-configuration/app-locales-and-device-timezones.md) to ensure consistent behavior across environments and regions.
* Explore all the [subcommand options for `cloud`.](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options#cloud)
