# Cloud Quickstart

Before wiring into CI, we recommend uploading a local build from your terminal to see the process working end-to-end. These steps should take you less than 5 minutes.

## 1. Install the Maestro CLI

We'll be using the `maestro cloud` command below to upload to Robin, so start by [**installing the Maestro CLI**](../getting-started/installing-maestro/) if you haven't already:

```
curl -Ls "https://get.maestro.mobile.dev" | bash
```

## 2. Retrieve your API Key and Project ID

Log in to Robin, click Settings and copy your Project ID. Please reach out to your mobile.dev representative to obtain your API key.

## 3. Download the Samples

Use the download-samples command to download a sample app and Flow file to upload to Robin:

```
maestro download-samples
```

You can of course choose to upload your own app and Flow file, but we recommend using the samples first to see how it works!

## 4. Run your Flow on Robin

Use the `maestro cloud` command to run your flow on Robin. This command works the same whether you're running it locally or in CI.

#### Android

```bash
cd ./samples
maestro cloud --api-key <ROBIN_API_KEY> --project-id <ROBIN_PROJECT_ID> sample.apk android-flow.yaml
```

#### iOS

```bash
cd ./samples
maestro cloud --api-key <ROBIN_API_KEY> --project-id <ROBIN_PROJECT_ID> sample.zip ios-flow.yaml
```

{% hint style="info" %}
Note that if you want to run any of the **advanced** examples you need to upload the full `samples` folder, since the advanced Flows make use of subflows. More information about subflows and what Flows to include can be found [here](../cli/test-suites-and-reports.md#controlling-what-tests-to-include).&#x20;
{% endhint %}

To run both Android Flows in Robin, you can for example run the following command outside of the `samples` folder.

```bash
maestro cloud samples/sample.apk samples
```

## 5. View results in Robin

A link to Robin is printed out after your Flow is uploaded successfully. Click on the link to view the results of your upload. It may take a minute or so before your results are ready.

## Congrats 🎉

Congrats, you just ran your first Flow on Robin! 🙌

Now that's you've seen how this works locally, let's take a look at how this can be integrated into your CI workflows:

{% content-ref url="ci-integration/" %}
[ci-integration](ci-integration/)
{% endcontent-ref %}
