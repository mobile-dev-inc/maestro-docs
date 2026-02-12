---
description: >-
  Integrate Maestro Cloud with any CI/CD provider using the CLI. Works with
  Jenkins, GitLab CI, Azure DevOps, and more.
---

# Generic CI platform

You can run Maestro Flows in the cloud from any CI platform by using the Maestro CLI. This flexible approach works with Jenkins, GitLab CI, Azure DevOps, and more.

{% hint style="info" %}
**Maestro Cloud Plan required.**

Cloud execution is available on the [Maestro Cloud Plan](https://signin.maestro.dev/sign-up).
{% endhint %}

{% hint style="info" %}
Refer to the appropriate guide if you are using one of the following CI/CD integration options:

* [github-actions](github-actions/ "mention")
* [bitrise.md](bitrise.md "mention")
* [bitbucket-pipelines.md](bitbucket-pipelines.md "mention")
* [circleci.md](circleci.md "mention")
{% endhint %}

### Prerequisites

* **API Key**: Get your API Key in the [Maestro Dashboard](https://app.maestro.dev/).
* **Project ID**: Obtain your Project ID from your project settings in the dashboard.
* **Build Compatibility**:
  * **Android**: APKs must be ARMv8 compatible.
  * **iOS**: Simulator builds must be provided as a `*.app` directory or a zipped `*.app`.

### Integration steps

{% stepper %}
{% step %}
#### Organize your Flows

Add your Flow files to a single directory in your repository.&#x20;

```
<root>
├── e2e/
│   ├── subflows/
│   │   └── LoginSubflow.yaml
│   ├── Login.yaml
│   └── Search.yaml
```

In this configuration, files in the root of `e2e` run as top-level Flows. Files in subdirectories can be used as subflows that are not executed, but can be used by other flows at the top level.
{% endstep %}

{% step %}
### &#x20;Install the Maestro CLI

Ensure the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/how-to-install-maestro-cli) is installed on your CI runner:

```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
```
{% endstep %}

{% step %}
### Run the cloud command

Execute the `maestro cloud` command as part of your pipeline.

```bash
maestro cloud \
  --api-key "<YOUR_API_KEY>" \
  --project-id "<YOUR_PROJECT_ID>" \
  --name "<uploadName>" \
  --app-file "<APP_FILE>" \
  --flows "./e2e"
```

The following table describes all the parameter you must pass:

| Parameter      | Description                                                                                                                                                                         |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--api-key`    | Your Maestro Cloud API Key.                                                                                                                                                         |
| `--project-id` | Your Maestro Project ID.                                                                                                                                                            |
| `--name`       | **(Optional)** A custom name for this specific upload.                                                                                                                              |
| `--app-file`   | Path to your `.apk` or `.app` binary. Check the [build-your-app-for-the-cloud.md](../build-your-app-for-the-cloud.md "mention") guide for more information on how to build the app. |
| `--flows`      | The directory containing your Flows.                                                                                                                                                |

{% hint style="info" %}
For a complete list of advanced flags, refer to the [Maestro CLI commands and options](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options "mention") reference.
{% endhint %}
{% endstep %}

{% step %}
### Handling results

Once your tests finish running, Maestro follows standard CI practices to let you know how they went:

* **Exit Codes**: The `maestro cloud` command returns `0` on success and `1` if any Flow fails. CI platforms typically use these exit codes to mark a build as failed.
* **Reports**: A link to the upload details in the Maestro Console is printed in the terminal logs for every run.
{% endstep %}
{% endstepper %}

#### Next steps

Now that your CI pipeline is connected, consider optimizing your cloud runs:

* Set up notifications via [Slack](../notifications/set-slack-notification.md), [email](../notifications/set-email-notification.md), or [webhooks](../notifications/configure-webhooks.md) to stay informed about build and test results.
* [Configure the operating system](../environment-configuration/configure-the-os.md) for your runs to match your application and dependency requirements.
* Define [locales and time zones](../environment-configuration/app-locales-and-device-timezones.md) to ensure consistent behavior across environments and regions.
