# GitHub Actions

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
name: Build and test (Native Android)

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

## Update your GitHub Actions workflow

Next, you’ll need to update your GitHub Actions workflow to add in the Maestro Cloud step. The workflows above execute generally the same steps for each platform:

* For every `push or pull_request` to `main` branch trigger this job
* Build the application
* Upload the built application and Flow files to Maestro Cloud
* Note the `MAESTRO_API_KEY` is the same secret you added to your Github repository earlier

### Usage examples

Below you can find various examples for different platforms for how to structure your GitHub action to build and upload your app to Maestro Cloud:

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

Check out the Maestro Cloud Action [README](https://github.com/mobile-dev-inc/action-maestro-cloud) for more information on how to configure the step.
