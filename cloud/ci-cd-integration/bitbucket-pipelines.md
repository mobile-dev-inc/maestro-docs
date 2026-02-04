---
description: >-
  Run Maestro tests in the cloud using Bitbucket Pipelines and the Maestro Cloud
  Pipe.
---

# Bitbucket Pipelines

Integrate Maestro Cloud into your Bitbucket CI/CD workflow using the [Maestro Cloud Upload Pipe](https://bitbucket.org/product/features/pipelines/integrations?search=maestro\&p=mobiledevinc/maestro-cloud-upload). This native integration allows you to automatically upload and execute your Flows on enterprise-grade infrastructure directly from your CI/CD pipeline.

{% hint style="info" %}
**Maestro Cloud Plan required.**

Bitbucket integration is available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

{% stepper %}
{% step %}
### Setup environment variables

To authenticate with Maestro Cloud, you must add your credentials as secret variables in Bitbucket.

1. On Bitbucket, navigate to your **Repository → Repository settings → Repository Variables**.
2. Add the following secured variables:
   * `MDEV_API_KEY`: Your Maestro Cloud API Key.
   * `MDEV_PROJECT_ID`: Your specific Maestro Project ID.

{% hint style="info" %}
Access the [Maestro Dashboard](https://app.maestro.dev/) to get your API Key and Project ID.
{% endhint %}
{% endstep %}

{% step %}
### Organize your Flows

Maestro expects your Flow files to be located in a specific directory (`.maestro/`) at the root of your repository.

1. Create a `.maestro/` directory at your repository root.
2. Place all Flow files directly inside `.maestro/` to be executed as a standalone test.
3. Place all "utility" Flows (those used by `runFlow`) in a `subflows/` subdirectory. This way you prevent these Flows from executing as top-level tests.

```
<root>
├── .maestro/
│   ├── subflows/
│   │   └── LoginSubFlow.yaml    # Only runs when called via runFlow
│   ├── Login.yaml               # Executed as a top-level Flow
│   ├── Add_to_Cart.yaml         # Executed as a top-level Flow
│   └── Search.yaml              # Executed as a top-level Flow
```
{% endstep %}

{% step %}
### Add the Maestro Cloud Pipe

Update your `bitbucket-pipelines.yml` file to include the [Maestro Cloud Upload Pipe](https://bitbucket.org/product/features/pipelines/integrations?search=maestro\&p=mobiledevinc/maestro-cloud-upload). This step should occur immediately after your app has successfully built.

{% hint style="warning" %}
All file paths provided below are relative to the repository source root.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
```yaml
script:
  - pipe: mobiledevinc/maestro-cloud-upload:1.0.0
    variables:
      MDEV_API_KEY: $MDEV_API_KEY
      MDEV_PROJECT_ID: $MDEV_PROJECT_ID
      MDEV_APP_FILE: app/build/outputs/apk/debug/app-debug.apk
```
{% endtab %}

{% tab title="iOS" %}
```yaml
script:
  - pipe: mobiledevinc/maestro-cloud-upload:1.0.0
    variables:
      MDEV_API_KEY: $MDEV_API_KEY
      MDEV_PROJECT_ID: $MDEV_PROJECT_ID
      MDEV_APP_FILE: <app_name>.app
```
{% endtab %}
{% endtabs %}

Once triggered, the Maestro Cloud Pipe automates the following lifecycle:

* Uploads your app binary and Flow workspace to Maestro Cloud.
* Runs your tests on dedicated cloud infrastructure.
* By default, the pipe waits for all Flows to complete. You can configure this option.
* Returns an exit code of `0` on success or `1` if failures are detected, allowing you to block builds based on test results.
{% endstep %}
{% endstepper %}
