---
hidden: true
---

# Migrating from Maestro Cloud

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

## Maestro Cloud to Robin Migration Guide

Welcome to the migration guide for transitioning from **Maestro Cloud** to **Robin**. This guide will help you update your integration—whether using a **Continuous Integration (CI) system** or the **Command Line Interface (CLI)**—with the necessary changes to smoothly switch to Robin.

***

{% hint style="info" %}
TLDR: simply update your CI integration / maestro CLI and pass your new Robin API key and project id along. Example:

```
maestro cloud --api-key <ROBIN_API_KEY> --project-id <ROBIN_PROJECT_ID> <appFile> <flows>
```
{% endhint %}

### Overview

If you’re migrating from **Maestro Cloud** to **Robin**, you will need to update either your CI integration or CLI tool with:

1. A new API key for Robin
2. The project ID for your project
3. Specify what iOS / Android API level if you don't want to run the Robin default (which is iOS 16 / Android API 33)

This documentation will walk you through the steps to obtain these and update your existing setups which can be completed in **minutes**.

### Step 1: Obtain your API Key

Please reach out to your mobile.dev representative to obtain your secret API key.

_Note: Treat your API key like a password. Do not share it publicly._

### Step 2: Obtain your your Project ID

1. Go to the Robin console
2. Navigate to Settings
3. Copy the Project ID

<figure><img src=".gitbook/assets/Screenshot 2024-10-16 at 09.49.09.png" alt=""><figcaption></figcaption></figure>

This project ID will be required in both your CI and CLI updates and is **not secret**.

### Step 3: Update your setup

**If you're using the Maestro CLI**

Simply use your new API key and pass `--project-id` along with the `maestro cloud` call and you'll be all set!

For example, the following command when using Maestro Cloud

```
maestro cloud --api-key <MAESTRO_CLOUD_API_KEY> <app> <flows>
```

updated to upload to Robin looks like this

```
maestro cloud --api-key <ROBIN_API_KEY> --project-id <ROBIN_PROJECT_ID> <app> <flows>
```

**If you're using a CI integration**

CI Integrations have been updated to support specifying the Robin Project ID - please refer to the [CI Integration docs](cloud/ci-integration/) to learn how to set up your specific CI integration with your new API Key and Robin Project ID.

**Updating device OS version**

{% hint style="warning" %}
Make sure that you specify the intended OS version - the defaults are different in Robin compared to Maestro Cloud
{% endhint %}

The default OS versions for Robin are iOS 16 and Android API level 33, which is different from Maestro Cloud, which had defaults of iOS 15 and API level 30.  Please refer to the docs below with information on how to configure OS version.

{% content-ref url="cloud/reference/configuring-os-version.md" %}
[configuring-os-version.md](cloud/reference/configuring-os-version.md)
{% endcontent-ref %}

### Troubleshooting

Here are some common issues and solutions:

* **Invalid API Key**: Ensure the API key is copied correctly and not expired.
* **Missing Project ID**: Double-check that the project ID in the Robin portal matches the one in your configuration.
* **Authentication Errors**: Verify that the API key has the correct permissions for the actions you're trying to perform.

For further assistance, consult the Robin support team or check the Robin Documentation.

***

By following these steps, you will successfully migrate from Maestro Cloud to Robin. If you encounter any issues, refer to the troubleshooting section or reach out to support.
