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

### Prerequisites

* **API Key**: Get your API Key in the [Maestro Dashboard](https://app.maestro.dev/).
* **Project ID**: Obtain your Project ID from your project settings in the dashboard.
* **Build Compatibility**:
  * **Android**: APKs must be x86 compatible.
  * **iOS**: Simulator builds must be provided as a `*.app` directory or a zipped `*.app`.

### Integration steps

{% stepper %}
{% step %}
#### Organize your Flows

Add your Flow files to a single directory in your repository. We recommend using `.maestro/` at the root level.

```
<root>
├── .maestro/
│   ├── subflows/
│   │   └── LoginSubflow.yaml
│   ├── Login.yaml
│   └── Search.yaml
```

Files in the root of `.maestro/` run as top-level Flows. Files in subdirectories can be used as subflows that are not executed, but can be used by other flows at the top level.
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
  --api-key <YOUR_API_KEY> \
  --project-id <YOUR_PROJECT_ID> \
   --name <uploadName> \
  <APP_FILE> .maestro/
```

The following table describes all the parameter you must pass:

| Parameter      | Description                                                                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--api-key`    | Your Maestro Cloud API Key.                                                                                                                                                      |
| `--project-id` | Your Maestro Project ID.                                                                                                                                                         |
| `--name`       | **(Optional)** Upload name.                                                                                                                                                      |
| `<APP_FILE>`   | Path to your APK or `.app` binary. Check the [build-your-app-for-the-cloud.md](../build-your-app-for-the-cloud.md "mention") guide for more information on how to build the app. |
| `.maestro/`    | The directory containing your Flows.                                                                                                                                             |
{% endstep %}

{% step %}
### Handling results

Once your tests finish running, Maestro follows standard CI practices to let you know how they went:

* **Exit Codes**: The `maestro cloud` command returns `0` on success and `1` if any Flow fails. CI platforms typically use these exit codes to mark a build as failed.
* **Reports**: A link to the upload details in the Maestro Console is printed in the terminal logs for every run.
{% endstep %}
{% endstepper %}
