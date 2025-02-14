# Integration with any CI platform

You can use the Maestro CLI to run your Flows on Robin from any CI platform.

## Prerequisites

<table data-header-hidden><thead><tr><th width="126"></th><th></th></tr></thead><tbody><tr><td><strong>API Key</strong></td><td>Reach out to your mobile.dev representative to obtain your Robin API key</td></tr><tr><td>Project ID</td><td>The id of the project you want to upload your app and Flows to. You can retrieve this from the Robin console.</td></tr><tr><td><strong>iOS</strong></td><td>Provide a path that points to an x86-compatible <code>*.app</code> simulator build directory, or a zipped file that contains the <code>*.app</code> build.</td></tr><tr><td><strong>Android</strong></td><td>You APK must be x86-compatible.</td></tr></tbody></table>

## 1.  Organize your Flows

Add all of your Flows under a single directory in your repo. We recommend naming this directory `.maestro/`  as this is the naming convention our native integrations expect by default. (Note the "." at the beginning of `.maestro/`)

```
<root>
├── .maestro/
│   ├── Login.yaml
│   ├── Add to Cart.yaml
│   └── Search.yaml
```

All of the flows directly under the `.maestro/` directory will be executed by Robin.

#### Subflows

It's common to have some Flow files that are only meant to be executed as part of another Flow via the `runFlow` command. These "subflows" can be nested under a subdirectory to prevent them from running as a top-level Flow.

```
<root>
├── .maestro/
│   ├── subflows/
│   │   └── MySubflow.yaml
│   ├── Login.yaml
│   ├── Add to Cart.yaml
│   └── Search.yaml
```

In the example above, `MySubflow.yaml` will not be executed as a top-level Flow, but still can be referenced by other Flows using the `runFlow` command.

## 2. Run Flows on Robin

#### 1. Install the Maestro CLI

First, ensure that the [Maestro CLI is installed](../../getting-started/installing-maestro/) on your CI machine:

```shell
curl -Ls "https://get.maestro.mobile.dev" | bash
```

#### 2. Run the "maestro cloud" command

Add a step in your CI workflow that executes the `maestro cloud` command:

```
maestro cloud --apiKey <apiKey> --project-id <projectId> <appFile> .maestro/
```

<table data-header-hidden><thead><tr><th width="144"></th><th></th></tr></thead><tbody><tr><td><strong>&#x3C;apiKey></strong></td><td>Robin API Key</td></tr><tr><td>&#x3C;projectId></td><td>Robin Project ID</td></tr><tr><td><strong>&#x3C;appFile></strong></td><td>The APK file or .app directory (<a href="broken-reference">instructions</a>)</td></tr><tr><td><strong>.maestro/</strong></td><td>The directory that contains your Flows</td></tr></tbody></table>

To set a name for your upload, use the `--name` option:

```
maestro cloud --apiKey <apiKey> --project-id <projectId> --name <uploadName> <appFi
```

{% hint style="info" %}
Note that you can also define your API key as an environment variable in your shell with the name `MAESTRO_CLOUD_API_KEY` and Maestro will automatically read it for you
{% endhint %}

## 3. Detect Flow Failures

The `maestro cloud` command and our native CI integrations will wait for your Flows to finish executing before returning.

If any Flow failures are detected, the exit code is set to 1. On success, the exit code will be set to 0. This allows you to leverage any existing test alerting you have in place.

## 4. View Result Details

A link to the current upload will be printed out to your logs. You can view any ongoing or past uploads in the Robin console.
