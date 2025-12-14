# Cloud Quickstart

Before wiring into CI, we recommend uploading a local build from your terminal to see the process working end-to-end. These steps should take you less than 5 minutes.

## 1. Install the Maestro CLI

We'll be using the `maestro cloud` command below to run your flows in the cloud, so start by [**installing the Maestro CLI**](../getting-started/installing-maestro/) if you haven't already:

```
curl -Ls "https://get.maestro.mobile.dev" | bash
```

## 2. Download the Samples

Use the download-samples command to download a sample app and Flow file:

```
maestro download-samples
```

You can of course choose to upload your own app and Flow file, but we recommend using the samples first to see how it works!

## 3. Run your Flow in the cloud

Use the `maestro cloud` command to run your flow in the cloud. This command works the same whether you're running it locally or in CI.

#### Android

```bash
cd ./samples
maestro cloud sample.apk android-flow.yaml
```

If you're a member of multiple organisation, or have multiple projects, you can optionally add `--api-key` and/or `--project-id` respectively to avoid being prompted for selection.

```bash
cd ./samples
maestro cloud sample.apk android-flow.yaml
```

#### iOS

```bash
cd ./samples
maestro cloud sample.app ios-flow.yaml
```

If you're a member of multiple organisation, or have multiple projects, you can optionally add `--api-key` and/or `--project-id` respectively to avoid being prompted for selection.

```bash
cd ./samples
maestro cloud --api-key <API_KEY> --project-id <PROJECT_ID> sample.zip ios-flow.yaml
```

To run any flow that depends on other files (like the **advanced** examples) you need to upload the full folder, so that Maestro has all of the files it needs. More information about subflows and what Flows to include can be found [here](../cli/test-suites-and-reports.md#controlling-what-tests-to-include).

## 4. View results in the console

A link to the Maestro console is printed out after your Flow is uploaded successfully. Click on the link to view the results of your upload. It may take a minute or so before your results are ready.

## Congrats 🎉

Congrats, you just ran your first Maestro Flow in the cloud! 🙌

Now that's you've seen how this works locally, let's take a look at how this can be integrated into your CI workflows:

{% content-ref url="ci-integration/" %}
[ci-integration](ci-integration/)
{% endcontent-ref %}
