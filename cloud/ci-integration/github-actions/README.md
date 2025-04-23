# GitHub Actions

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

Maestro cloud testing is compatible with all CI systems and provides native integrations with a number of common providers including GitHub Actions. You can start running your Flows in CI with just a few lines of configuration using the [Maestro Cloud GitHub Action](http://github.com/mobile-dev-inc/action-maestro-cloud).

## Setup

#### Add your API key secret

The GitHub Action will need to authenticate with your Maestro account. So the first step is to expose your API key as a GitHub “Repository Secret”.

**Add your API key as a “Repository Secret”**

1. Navigate to your GitHub repo and click on Settings in top nav bar.
2. In repository settings page click on `Secrets -> Actions`. It will open Action Secrets page.
3. On Action Secrets page, click on `New Repository Secret` button. Use `MAESTRO_API_KEY` as the secret name and paste your Maestro API key from the previous step into the “Secret” value text box. Click “Add Secret” to add the secret.

**Add your Project ID**

The project ID is not a secret, so you either specify it as `project-id` in your workflow file or you add it as an env variable.

**Other setup**

Please refer to the Action documentation [here](https://github.com/marketplace/actions/maestro-cloud-upload-action) to see all configuration options.

## Example

```yaml
name: Build and run Maestro tests (Native Android)

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  maestro-cloud:
    runs-on: ubuntu-latest
    outputs:
      app: app/build/outputs/apk/debug
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: 11
          distribution: 'temurin'
      - run: ./gradlew assembleDebug
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: app/build/outputs/apk/debug/app-debug.apk
```

## Commit your Maestro Flows to your repository

Create a `.maestro/` directory at the root of your repository and commit your Flows there:

```
<root>
├── .maestro/
│   ├── Login.yaml
│   ├── Add to Cart.yaml
│   └── Search.yaml
```

It’s common to have some Flow files that are only meant to be executed as part of another Flow via the `runFlow` command. These "subflows" can be nested under a subdirectory to prevent them from running as a top-level Flow.

```
<root>
├── .maestro/
│   ├── subflows/
│   │   └── MySubflow.yaml
│   ├── Login.yaml
│   ├── Add to Cart.yaml
│   └── Search.yaml
```

## Inputs

| Key                 | Required                 | Description                                                                     |
|---------------------|--------------------------|-------------------------------------------------------------------------------- |
| `api-key`           | Yes                      | Your Maestro Cloud API key                                                      |
| `android-api-level` | No                       | The Android API level to use when running the Flows                             |
| `app-file`          | Yes (or `app-binary-id`) | Path to the app file to upload.                                                 |
| `app-binary-id`     | Yes (or `app-file`)      | The ID of a previously uploaded app-file.                                       |
| `async`             | No                       | Whether to start the flow and exit the action (defaults to `false`)             |
| `env`               | No                       | Environment variables to pass to the run                                        |
| `exclude-tags`      | No                       | Comma-separated list of tags to exclude from the run                            |
| `include-tags`      | No                       | Comma-separated list of tags to include in the run                              |
| `mapping-file`      | No                       | Path to the ProGuard map (Android) or dSYM (iOS)                                |
| `project-id`        | Yes                      | Which project to run the tests against                                          |
| `name`              | No                       | Friendly name of the run                                                        |
| `timeout`           | No                       | How long to wait for the run to complete when not async (defaults to 30 minutes)|
| `workspace`         | No                       | Path to the workspace directory containing the Flows (defaults to `.maestro`)   |
| `device-model`      | No                       | The [device model](https://docs.maestro.dev/cloud/reference/configuring-os-version#using-a-specific-ios-minor-version-and-device-recommended) to use when running the Flows (eg iPhone-11)                   |
| `device-os`         | No                       | The [device OS](https://docs.maestro.dev/cloud/reference/configuring-os-version) to use when running the Flows (eg iOS-16-2)                       |
| `device-locale`     | No                       | The [device locale](https://docs.maestro.dev/cloud/reference/configuring-device-locale) to use when running the Flows (eg en_US)                      |

## Custom workspace location

By default, the action is looking for a `.maestro` folder with Maestro flows in the root directory of the project. If you would like to customize this behaviour, you can override it with a `workspace` argument:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    workspace: myFlows/
```

## Custom name

A name will automatically be provided according to the following order:

1. If it is a Pull Request, use Pull Request title as name
2. If it is a normal push, use commit message as name
3. If for some reason the commit message is not available, use the commit SHA as name

If you want to override this behaviour and specify your own name, you can do so by setting the `name` argument:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    name: My Upload
```

## Run in async mode

If you don't want the action to wait until the Upload has been completed as is the default behaviour, set the `async` argument to `true`:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    async: true
```

Alternatively, you might want to still wait for the action but would like to configure the timeout period, set `timeout` argument to a number of minutes:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    timeout: 90 # Wait for 90 minutes
```

## Triggers

Trigger this action on (1) pushes to your main branch and (2) pull requests opened against your main branch:

```yaml
on:
  push:
    branches: [master]
  pull_request:
    branches: [master]
```

If you need to use the `pull_request_target` trigger to support repo forks, check out the HEAD of the pull request to ensure that you're running the analysis against the changed code:

```yaml
on:
  push:
    branches: [master]
  pull_request_target:
    branches: [master]
jobs:
  upload-to-mobile-dev:
    name: Run Flows on Maestro Cloud
    steps:
      - uses: actions/checkout@v3
        with:
          ref: ${{ github.event.pull_request.head.sha }} # Checkout PR HEAD
```

For more information on triggering workflows, check out [GitHub's documentation](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows).

## Adding environment variables

If you want to pass environment variables along with your upload, add a multiline `env` argument:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    env: |
      USERNAME=<username>
      PASSWORD=<password>
```

## Using tags

You can use Maestro [Tags](https://maestro.mobile.dev/cli/tags) to filter which Flows to send:

You can either pass a single value, or comma-separated (`,`) values.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    include-tags: dev, pull-request
    exclude-tags: excludeTag
```



## Using an already uploaded App

You can use an already uploaded binary in Maestro Cloud using the `app-binary-id` parameter.

```yaml
      - id: upload
        uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          project-id: 'proj_01example0example1example2'
          app-file: app.zip

      - uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          project-id: 'proj_01example0example1example2'
          app-binary-id: ${{ steps.upload.outputs.MAESTRO_CLOUD_APP_BINARY_ID }}
```

## Configuring the locale for the device where the flows will be executed

To switch the device locale on a remote device from a default one (en_US) `device-locale` parameter should be used. The value is a combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code, i.e. "de_DE" for Germany.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    device-locale: de_DE

```

## Outputs

The following output variables are set by the action:

- `MAESTRO_CLOUD_CONSOLE_URL` - link to the Maestro Cloud console (if using Maestro Cloud)
- `MAESTRO_CLOUD_UPLOAD_STATUS` - status of the Upload (not available in `async` mode)
- `MAESTRO_CLOUD_FLOW_RESULTS` - list of Flows and their results (not available in `async` mode)
- `MAESTRO_CLOUD_APP_BINARY_ID` - id of the binary uploaded (if using Maestro Cloud)

In order to access these variables you can use the following approach:

```yaml
- id: upload
  uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: <your_app_file>
    # ... any other parameters

- name: Access Outputs
  if: always()
  run: |
    echo "Console URL: ${{ steps.upload.outputs.MAESTRO_CLOUD_CONSOLE_URL }}"
    echo "Flow Results: ${{ steps.upload.outputs.MAESTRO_CLOUD_FLOW_RESULTS }}"
    echo "Upload Status: ${{ steps.upload.outputs.MAESTRO_CLOUD_UPLOAD_STATUS }}"
    echo "App Binary ID: ${{ steps.upload.outputs.MAESTRO_CLOUD_APP_BINARY_ID }}"
```

### Output types

- `MAESTRO_CLOUD_UPLOAD_STATUS`

  Any of the following values:

  ```plaintext
  PENDING
  PREPARING
  INSTALLING
  RUNNING
  SUCCESS
  ERROR
  CANCELED
  WARNING
  STOPPED
  ```

- `MAESTRO_CLOUD_FLOW_RESULTS`

   An array of objects with at least `name`, `status`, and `errors` fields.

   ```json
   [{"name":"my-first-flow","status":"SUCCESS","errors":[]},{"name":"my-second-flow","status":"SUCCESS","errors":[]},{"name":"my-cancelled-flow","status":"CANCELED","errors":[],"cancellationReason":"INFRA_ERROR"}]
   ```


### Usage examples

Below you can find various examples and additional configuration options for different platforms for how to structure your GitHub action to build and upload your app to Maestro Cloud:

{% content-ref url="maestro-github-action-for-android.md" %}
[maestro-github-action-for-android.md](maestro-github-action-for-android.md)
{% endcontent-ref %}

{% content-ref url="maestro-github-action-for-ios.md" %}
[maestro-github-action-for-ios.md](maestro-github-action-for-ios.md)
{% endcontent-ref %}

{% content-ref url="maestro-github-action-for-flutter.md" %}
[maestro-github-action-for-flutter.md](maestro-github-action-for-flutter.md)
{% endcontent-ref %}

## That’s it!
