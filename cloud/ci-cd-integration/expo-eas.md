---
description: >-
  Run Maestro Flows from EAS Workflows with the maestro-cloud and maestro
  pre-packaged jobs. Set up the API key, Project ID, and build jobs for Android
  and iOS.
---

# Expo EAS Workflows

[EAS Workflows](https://docs.expo.dev/eas/workflows/get-started/) includes 2 pre-packaged jobs that run Maestro Flows against an app built by an EAS `build` job:

* `maestro-cloud`: uploads the build and your Flows to Maestro Cloud and runs them on Maestro Cloud devices.
* `maestro`: runs your Flows on an Android Emulator or iOS Simulator on EAS workers.

This guide covers both jobs, with a focus on `maestro-cloud`. For the full reference, see [Pre-packaged jobs](https://docs.expo.dev/eas/workflows/pre-packaged-jobs/) in the Expo documentation.

{% hint style="info" %}
**Maestro Cloud Plan required.**

The `maestro-cloud` job requires a Maestro Cloud account on the [Maestro Cloud Plan](https://signin.maestro.dev/sign-up). The `maestro` job runs on EAS workers and does not use Maestro Cloud.
{% endhint %}

### Prerequisites

* **Maestro Cloud Plan**: Required for the `maestro-cloud` job.
* **API key**: Get your API key in the [Maestro Dashboard](https://app.maestro.dev/) **Settings**.
* **Project ID**: Open the **Settings** menu in the [Maestro Dashboard](https://app.maestro.dev/) and select the project to see its ID.
* **A project configured for EAS Build**: Your **eas.json** must contain the build profile the workflow uses. See [Configure EAS Build](https://docs.expo.dev/build/setup/) in the Expo documentation.

### Integration steps

{% stepper %}
{% step %}
### Store the API key in EAS

The `maestro-cloud` job reads the API key from the `MAESTRO_CLOUD_API_KEY` environment variable by default. You can also pass it with the `maestro_api_key` parameter.

1. In the Expo dashboard, open your project's [Environment variables](https://expo.dev/accounts/\[account]/projects/\[project]/environment-variables) page.
2. Add a variable named `MAESTRO_CLOUD_API_KEY` with your Maestro Cloud API key as the value.
3. Set its visibility to **Secret**. Secret variables are not readable outside of the EAS servers and are obfuscated in EAS Workflows job logs.
4. Add it to the environment the job runs in. The `maestro` and `maestro-cloud` jobs use the `preview` environment unless you set `environment` on the job.
{% endstep %}

{% step %}
### Add a build profile for testing

Maestro needs an `.apk` for Android and a simulator `.app` for iOS. In **eas.json**, add a build profile that produces both:

```json
{
  "build": {
    "e2e-test": {
      "withoutCredentials": true,
      "ios": {
        "simulator": true
      },
      "android": {
        "buildType": "apk"
      }
    }
  }
}
```

{% hint style="info" %}
Maestro Cloud runs Android apps from ARM APKs. Check the [build-your-app-for-the-cloud.md](../build-your-app-for-the-cloud.md "mention") guide for the binary requirements.
{% endhint %}
{% endstep %}

{% step %}
### Organize your Flows

Add your Flow files to a single directory in your repository, for example `.maestro/` at the same level as **eas.json**.

```
<root>
├── eas.json
├── .maestro/
│   ├── subflows/
│   │   └── LoginSubflow.yaml
│   ├── Login.yaml
│   └── Search.yaml
```

{% hint style="success" %}
#### Subflows

Files in subdirectories (like `subflows/`) will not be executed as top-level tests, but can be called by other Flows using the `runFlow` command.
{% endhint %}
{% endstep %}

{% step %}
### Create the workflow

Create a `.eas/workflows/` directory at the root of your project and add a workflow file. A `build` job produces the app, and the Maestro job reads its ID from the `build_id` output with `${{ needs.<build_job_id>.outputs.build_id }}`. The `needs` keyword makes the Maestro job wait until the build job succeeds.

{% tabs %}
{% tab title="Maestro Cloud" %}
This workflow builds Android and iOS on every pull request and runs the Flows in `.maestro/` on Maestro Cloud.

```yaml
# .eas/workflows/maestro-cloud.yml
name: Maestro Cloud tests

on:
  pull_request:
    branches: ['*']

jobs:
  build_android:
    name: Build Android
    type: build
    params:
      platform: android
      profile: e2e-test

  build_ios:
    name: Build iOS
    type: build
    params:
      platform: ios
      profile: e2e-test

  maestro_cloud_android:
    name: Maestro Cloud (Android)
    needs: [build_android]
    type: maestro-cloud
    environment: preview
    params:
      build_id: ${{ needs.build_android.outputs.build_id }}
      maestro_project_id: <YOUR_PROJECT_ID>
      flows: ./.maestro
      device_model: pixel_6
      device_os: android-34

  maestro_cloud_ios:
    name: Maestro Cloud (iOS)
    needs: [build_ios]
    type: maestro-cloud
    environment: preview
    params:
      build_id: ${{ needs.build_ios.outputs.build_id }}
      maestro_project_id: <YOUR_PROJECT_ID>
      flows: ./.maestro
      device_model: iPhone-17-Pro
      device_os: iOS-26-2
```
{% endtab %}

{% tab title="EAS workers" %}
This workflow builds Android and iOS on every pull request and runs the Flows in `.maestro/` on EAS workers.

```yaml
# .eas/workflows/maestro-eas.yml
name: Maestro tests on EAS

on:
  pull_request:
    branches: ['*']

jobs:
  build_android:
    name: Build Android
    type: build
    params:
      platform: android
      profile: e2e-test

  build_ios:
    name: Build iOS
    type: build
    params:
      platform: ios
      profile: e2e-test

  maestro_android:
    name: Maestro (Android)
    needs: [build_android]
    type: maestro
    runs_on: linux-medium-nested-virtualization
    params:
      build_id: ${{ needs.build_android.outputs.build_id }}
      flow_path: ./.maestro

  maestro_ios:
    name: Maestro (iOS)
    needs: [build_ios]
    type: maestro
    params:
      build_id: ${{ needs.build_ios.outputs.build_id }}
      flow_path: ./.maestro
```
{% endtab %}
{% endtabs %}

Replace `<YOUR_PROJECT_ID>` with your Maestro Project ID.
{% endstep %}

{% step %}
### Run the workflow

The workflows above run automatically when someone opens a pull request. You can also start a workflow manually with the EAS CLI:

```bash
eas workflow:run .eas/workflows/maestro-cloud.yml
```
{% endstep %}
{% endstepper %}

### Choose a job

| | `maestro-cloud` | `maestro` |
| --- | --- | --- |
| Where Flows run | Maestro Cloud devices | Android Emulator or iOS Simulator on EAS workers |
| Device selection | `device_model` and `device_os`, from `maestro list-cloud-devices` | `device_identifier` and `android_system_image_package` |
| Results | Maestro Cloud dashboard, plus job outputs in EAS | Job logs and the "Maestro Test Results" artifact in EAS |
| Maestro Cloud Plan | Required | Not required |

Use the `maestro` job when you run a small suite inside a pipeline that already runs on EAS. Use the `maestro-cloud` job when you want to run Flows in parallel across device models and OS versions on Maestro Cloud, and review results in the Maestro Cloud dashboard.

### The `maestro-cloud` job

The `maestro-cloud` job uploads the build and your Flows to Maestro Cloud. Most parameters map to a [`maestro cloud`](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options#cloud) option.

```yaml
jobs:
  run_maestro_tests:
    type: maestro-cloud
    environment: production | preview | development # optional, defaults to preview
    image: string # optional
    params:
      build_id: string # required
      maestro_project_id: string # required
      flows: string # required
      maestro_api_key: string # optional, defaults to $MAESTRO_CLOUD_API_KEY
      include_tags: string | string[] # optional
      exclude_tags: string | string[] # optional
      maestro_version: string # optional
      maestro_config: string # optional
      device_locale: string # optional
      device_model: string # optional
      device_os: string # optional
      skip_build_check: boolean # optional, defaults to false
      name: string # optional
      branch: string # optional
      async: boolean # optional
    hooks:
      after_checkout: step[] # optional
      before_maestro_cloud: step[] # optional
      after_maestro_cloud: step[] # optional
```

#### Parameters

| Parameter            | Required | Description                                                                                                                                                                  |
| -------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `build_id`           | Yes      | ID of the build to test. Example: `${{ needs.build_android.outputs.build_id }}`.                                                                                             |
| `maestro_project_id` | Yes      | Your Maestro Project ID. Maps to `--project-id`.                                                                                                                             |
| `flows`              | Yes      | Path to a Flow file or a directory of Flows. Maps to `--flows`.                                                                                                              |
| `maestro_api_key`    | No       | Your Maestro Cloud API key. Defaults to the `MAESTRO_CLOUD_API_KEY` environment variable. Maps to `--api-key`.                                                               |
| `include_tags`       | No       | Only run Flows with these tags. Maps to `--include-tags`. Example: `"pull,push"`.                                                                                            |
| `exclude_tags`       | No       | Skip Flows with these tags. Maps to `--exclude-tags`. Example: `"disabled"`.                                                                                                 |
| `maestro_version`    | No       | Maestro CLI version to use. Defaults to the version preinstalled on the image, or the latest version if none is found. Set to `latest` to always install the newest version. |
| `maestro_config`     | No       | Path to a Maestro `config.yaml` file. Maps to `--config`. Example: `.maestro/config.yaml`.                                                                                   |
| `device_locale`      | No       | Device locale. Maps to `--device-locale`. Example: `de_DE`.                                                                                                                  |
| `device_model`       | No       | Device model to run against. Maps to `--device-model`. Example: `pixel_6`, `iPhone-17-Pro`.                                                                                  |
| `device_os`          | No       | OS version to run against. Maps to `--device-os`. Example: `android-34`, `iOS-26-2`.                                                                                         |
| `skip_build_check`   | No       | Skip the check that an iOS build is a simulator build. Defaults to `false`.                                                                                                  |
| `name`               | No       | Name of the upload. Maps to `--name`.                                                                                                                                        |
| `branch`             | No       | Branch the upload originated from. When the workflow run is triggered from GitHub, EAS uses the run's branch by default. Maps to `--branch`.                                 |
| `async`              | No       | Exit after the upload without waiting for results. When `true`, the job status only shows whether the upload succeeded. Maps to `--async`.                                   |

#### Hooks

* `after_checkout`: steps to run after the job checks out your project.
* `before_maestro_cloud`: steps to run before the Maestro Cloud upload.
* `after_maestro_cloud`: steps to run after the Maestro Cloud upload.

#### Outputs

A later job that lists the Maestro job in `needs` or `after` can read these outputs, for example with `${{ after.maestro_cloud_android.outputs.maestro_cloud_url }}`.

| Output                       | Description                                                       |
| ---------------------------- | ----------------------------------------------------------------- |
| `maestro_cloud_url`          | URL of the upload results page in Maestro Cloud.                  |
| `total_flows_count`          | Number of Flows that ran.                                         |
| `successful_flows_count`     | Number of Flows with status `SUCCESS` or `WARNING`.               |
| `failed_flows_count`         | Number of Flows with status `ERROR` or `STOPPED`.                 |
| `successful_flow_names_json` | JSON array with the names of the successful Flows.                |
| `failed_flow_names_json`     | JSON array with the names of the failed Flows.                    |

{% hint style="info" %}
With `async: true`, only `maestro_cloud_url` is guaranteed to be valid. The other outputs can be empty because the job does not wait for the Flows to run.
{% endhint %}

### The `maestro` job

The `maestro` job runs your Flows on EAS workers. Expo marks this job as [alpha](https://docs.expo.dev/more/release-statuses/#alpha).

```yaml
jobs:
  run_maestro_tests:
    type: maestro
    environment: production | preview | development # optional, defaults to preview
    image: string # optional
    runs_on: string # optional
    params:
      build_id: string # required
      flow_path: string | string[] # required
      shards: number # optional, defaults to 1
      retries: number # optional, defaults to 0
      retry_failed_only: boolean # optional, defaults to true
      record_screen: boolean # optional, defaults to false
      include_tags: string | string[] # optional
      exclude_tags: string | string[] # optional
      maestro_version: string # optional
      android_system_image_package: string # optional
      device_identifier: string | { android?: string, ios?: string } # optional
      output_format: string # optional, defaults to junit
      skip_build_check: boolean # optional, defaults to false
    hooks:
      after_checkout: step[] # optional
      before_maestro_tests: step[] # optional
      after_maestro_tests: step[] # optional
```

#### Parameters

| Parameter                      | Required | Description                                                                                                                                                                  |
| ------------------------------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `build_id`                     | Yes      | ID of the build to test.                                                                                                                                                     |
| `flow_path`                    | Yes      | Path to the Flow files or directory to run. Accepts a string or a list.                                                                                                      |
| `shards`                       | No       | Number of shards to split the tests into. Experimental. Defaults to `1`.                                                                                                     |
| `retries`                      | No       | Number of times to retry the tests if they fail. Defaults to `0`.                                                                                                            |
| `retry_failed_only`            | No       | When `true`, retries re-run only the Flows that failed on the previous attempt, when applicable. Set to `false` to re-run all Flows. Defaults to `true`.                     |
| `record_screen`                | No       | Record the screen. Defaults to `false`. Recording can affect emulator performance.                                                                                           |
| `include_tags`                 | No       | Only run Flows with these tags. Passed to Maestro as `--include-tags`.                                                                                                       |
| `exclude_tags`                 | No       | Skip Flows with these tags. Passed to Maestro as `--exclude-tags`.                                                                                                           |
| `maestro_version`              | No       | Maestro CLI version to use. Defaults to the version preinstalled on the image, or the latest version if none is found. Set to `latest` to always install the newest version. |
| `android_system_image_package` | No       | Android Emulator system image package. Use an `x86_64` variant. Example: `system-images;android-36;google_apis;x86_64`.                                                      |
| `device_identifier`            | No       | Device to use. Accepts a string such as `pixel_6` or an object such as `{ android: "pixel_6", ios: "iPhone 16 Plus" }`. Available iOS devices depend on the runner image.    |
| `output_format`                | No       | Test report format. Passed to Maestro as `--format`. Defaults to `junit`.                                                                                                    |
| `skip_build_check`             | No       | Skip the check that an iOS build is a simulator build. Defaults to `false`.                                                                                                  |

#### Hooks

* `after_checkout`: steps to run after the job checks out your project.
* `before_maestro_tests`: steps to run before the tests start.
* `after_maestro_tests`: steps to run after the tests complete.

{% hint style="info" %}
Android Emulator jobs need a `linux-*-nested-virtualization` worker, set with `runs_on`. iOS Simulator jobs need a `macos-*` worker. See [`runs_on`](https://docs.expo.dev/eas/workflows/syntax/#jobsjob_idruns_on) in the Expo documentation.
{% endhint %}

### Find device models and OS versions

The `device_model` and `device_os` values for the `maestro-cloud` job are the same values the `maestro cloud` command accepts. To list them, run:

```bash
maestro list-cloud-devices
```

The command lists the devices available on Maestro Cloud, grouped by platform. For more details, see [Configure the OS](../environment-configuration/configure-the-os.md).

### View results

* **Maestro Cloud dashboard**: Each `maestro-cloud` run creates an upload in the [Maestro Dashboard](https://app.maestro.dev/). The `maestro_cloud_url` output links to its results page.
* **EAS workflow run**: Each job shows its status and logs in the EAS dashboard. Without `async`, a `maestro-cloud` job fails when Flows fail.
* **EAS artifacts**: For the `maestro` job, screenshots and recordings saved by your Flows are available in the "Maestro Test Results" artifact.

### Troubleshooting

* **Missing API key**: Set the `maestro_api_key` parameter or the `MAESTRO_CLOUD_API_KEY` environment variable. Check that the variable exists in the environment the job runs in, which is `preview` unless you set `environment`.
* **iOS build check fails**: Unless `skip_build_check` is `true`, both jobs check that an iOS build is a simulator build. Use a build profile with `"ios": { "simulator": true }`.
* **Unsupported device**: Run `maestro list-cloud-devices` and use a `device_model` and `device_os` value from its output.
* **Job passes but Flows failed**: With `async: true`, the job status only reflects the upload. Check the results in the Maestro Dashboard, or remove `async` to make the job wait for the Flows.
* **Android Emulator jobs on EAS workers**: Set `runs_on` to a `linux-*-nested-virtualization` worker on the `maestro` job.

#### Next steps

Now that your CI pipeline is connected, consider optimizing your cloud runs:

* Set up notifications via [Slack](../notifications/set-slack-notification.md), [email](../notifications/set-email-notification.md), or [webhooks](../notifications/configure-webhooks.md) to stay informed about build and test results.
* [Configure the operating system](../environment-configuration/configure-the-os.md) for your runs to match your application and dependency requirements.
* Define [locales and time zones](../environment-configuration/app-locales-and-device-timezones.md) to ensure consistent behavior across environments and regions.
* Explore all the [subcommand options for `cloud`.](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options#cloud)
