# GitHub Actions

Maestro Cloud provides a native [GitHub Action](https://github.com/marketplace/actions/maestro-cloud-upload-action) that allows you to easily integrate mobile UI testing into your GitHub workflows.

Maestro Cloud has a integration with GitHub Actions that allows you to automate your mobile and web testing pipelines. By using the official [Maestro Cloud GitHub Action](https://github.com/marketplace/actions/maestro-cloud-upload-action), you can trigger tests on every push or pull request and view results directly in the Maestro Console.

{% hint style="info" %}
**Maestro Cloud Plan required.**&#x20;

GitHub Actions integration is available on the [Maestro Cloud Plan](https://signin.maestro.dev/sign-up).
{% endhint %}

### Setup

{% stepper %}
{% step %}
#### Add your API key secret

The GitHub Action requires an API key to authenticate with Maestro Cloud. You must expose your API key as a [GitHub Repository Secret](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets):

1. Navigate to your GitHub repository and click **Settings**.
2. In the sidebar, click **Secrets and variables** > **Actions**.
3. Click **New repository secret**.
4. Name the secret `MAESTRO_API_KEY` and paste your API key from the [Maestro Console](https://console.maestro.dev/) into the **Secret** field.
5. Click **Add secret**.
{% endstep %}

{% step %}
#### Add your Project ID


{% endstep %}
{% endstepper %}



#### 2. Add your Project ID

You can find your Project ID in the **Settings** section of the [Maestro Console](https://console.maestro.dev/). While not a secret, you can also store it as a Repository Secret (e.g., `MAESTRO_PROJECT_ID`) for convenience.

### Basic usage

By default, the action looks for a `.maestro/` folder at the root of your repository containing your Flow files.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: path/to/your/app.apk
```

### Usage examplesBuild your APK and upload it to Maestro Cloud.

````yaml
name: Maestro Android Test
on: [push]

jobs:
  maestro-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          java-version: 17
          distribution: 'temurin'
      - run: ./gradlew assembleDebug
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_API_KEY }}
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: app/build/outputs/apk/debug/app-debug.apk
```</div><div data-gb-custom-block data-tag="tab" data-title='iOS'>Build your iOS Simulator app (x86 or ARM) and upload it to Maestro Cloud.

```yaml
name: Maestro iOS Test
on: [push]

jobs:
  maestro-test:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4
      - run: xcodebuild build -scheme 'MyApp' -configuration Debug -destination 'generic/platform=iOS Simulator' CONFIGURATION_BUILD_DIR=$PWD/build
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_API_KEY }}
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: build/MyApp.app
```</div><div data-gb-custom-block data-tag="tab" data-title='Flutter'>Build your Flutter app for Android or iOS and upload it to Maestro Cloud.

```yaml
name: Maestro Flutter Test
on: [push]

jobs:
  maestro-test:
    runs-on: ubuntu-latest # Use macos-latest for iOS
    steps:
      - uses: actions/checkout@v4
      - uses: subosito/flutter-action@v2
        with:
          channel: 'stable'
      - run: flutter build apk --debug # Or: flutter build ios --debug --simulator
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_API_KEY }}
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: build/app/outputs/flutter-apk/app-debug.apk
```</div></div>

## Inputs

| Input | Required | Description |
| :--- | :--- | :--- |
| `api-key` | **Yes** | Your Maestro Cloud API Key. |
| `project-id` | **Yes** | Your Maestro Project ID. |
| `app-file` | **Yes*** | Path to your `.apk` or `.app` file. *Required unless `app-binary-id` is used. |
| `app-binary-id` | No | ID of a previously uploaded app binary. |
| `workspace` | No | Path to your Flows directory (defaults to `.maestro/`). |
| `async` | No | If `true`, the action returns immediately after starting the run (defaults to `false`). |
| `timeout` | No | Run timeout in minutes (defaults to 30). |
| `name` | No | Custom name for the run. |
| `env` | No | Custom environment variables for the run. |
| `include-tags` | No | Comma-separated tags to include. |
| `exclude-tags` | No | Comma-separated tags to exclude. |
| `device-model` | No | Specific device model (e.g., `iPhone-11`). |
| `device-os` | No | Specific OS version (e.g., `iOS-16-2`). |
| `device-locale` | No | Device locale (e.g., `en_US`). |
| `mapping-file` | No | Path to ProGuard mapping (Android) or dSYM (iOS) files. |

## Advanced configuration

### Custom name and workspace

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: app.apk
    workspace: custom-flows/
    name: "Nightly Regression Run"
````

#### Environment variables

Pass parameters to your Flows using the `env` input as a multiline string.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: app.apk
    env: |
      USERNAME: testuser
      PASSWORD: ${{ secrets.TEST_PASSWORD }}
```

#### Pull request triggers

Standard triggers for pushes and pull requests:

```yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```

If you use `pull_request_target` to support repository forks, check out the HEAD of the pull request:

```yaml
steps:
  - uses: actions/checkout@v4
    with:
      ref: ${{ github.event.pull_request.head.sha }}
```

### Outputs

The action sets the following outputs:

| Output                        | Description                                                 |
| ----------------------------- | ----------------------------------------------------------- |
| `MAESTRO_CLOUD_CONSOLE_URL`   | Link to the run in the Maestro Console.                     |
| `MAESTRO_CLOUD_UPLOAD_STATUS` | Final status of the upload (not available in `async` mode). |
| `MAESTRO_CLOUD_FLOW_RESULTS`  | JSON array of Flow results (not available in `async` mode). |
| `MAESTRO_CLOUD_APP_BINARY_ID` | The ID of the uploaded app binary.                          |

#### Accessing outputs

```yaml
- id: maestro-upload
  uses: mobile-dev-inc/action-maestro-cloud@v1
  # ... options

- name: Report Results
  if: always()
  run: |
    echo "Console URL: ${{ steps.maestro-upload.outputs.MAESTRO_CLOUD_CONSOLE_URL }}"
    echo "Status: ${{ steps.maestro-upload.outputs.MAESTRO_CLOUD_UPLOAD_STATUS }}"
```
