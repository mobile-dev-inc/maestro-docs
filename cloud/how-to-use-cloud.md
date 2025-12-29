# How to run your tests on Maestro Cloud

This guide explains how to execute your automated tests using Maestro Cloud via the Maestro CLI. You'll learn how to prepare your environment, upload test artifacts, and interpret results.

## Prerequisites

Ensure the following before proceeding:

- **Maestro CLI** is installed.
- You have an active **Maestro Cloud** account with appropriate permissions.

## Download sample projects

To get started quickly, download the official sample projects provided by Maestro:

```bash
maestro download-samples
```

This command retrieves a set of sample apps and flow files for both Android and iOS, which you can use to validate your setup.

## Running flows in the Google Cloud Platform

The `maestro cloud` command uploads your app and flow files to Maestro Cloud and starts the test run.

### Android example

```bash
cd samples
maestro cloud sample.apk android-flow.yaml
```

{% hint style="warning" %}
If you belong to multiple organizations or projects, specify your credentials to avoid interactive prompts:

```bash
maestro cloud --api-key <API_KEY> --project-id <PROJECT_ID> sample.apk android-flow.yaml
```

{% endhint %}}

### iOS example

```bash
cd samples
maestro cloud sample.app ios-flow.yaml
```

{% hint style="warning" %}

If your flow references additional files (for example, assets or configs), compress the entire folder and upload it as a `.zip` to ensure all dependencies are available during execution.

```bash
maestro cloud --api-key <API_KEY> --project-id <PROJECT_ID> sample.zip ios-flow.yaml
```
{% endhint %}

## View the Test Results

After a successful upload, the CLI outputs a link to the Maestro Cloud console. Open this link in your browser to monitor execution status, view logs, and analyze results. Test processing may take a few minutes depending on queue and app size.