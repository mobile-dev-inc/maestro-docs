---
description: >-
  Use --app-binary-id to skip re-uploading your app and save time. Find the
  binary ID in CLI output or Maestro dashboard.
---

# Reuse app binary

To run multiple test scenarios on the same build, you can reuse a previously uploaded binary instead of re-uploading the same file. This optimization saves time and bandwidth.

{% hint style="info" %}
**Maestro Cloud Plan required** App binary reuse is available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Find the app binary ID

When you upload an app to Maestro Cloud, a unique app binary ID is generated. You can find this ID in two locations:

* **CLI output**: The ID is returned in the terminal response immediately after a successful upload.

<figure><img src="../.gitbook/assets/cli-app-binary-id.png" alt=""><figcaption></figcaption></figure>

* **Maestro dashboard**: The ID is visible at the top of the run details page.

<figure><img src="../.gitbook/assets/dashboard-binary-app.png" alt=""><figcaption></figcaption></figure>

### Use the app binary ID

Use the `--app-binary-id` flag to reference a cached binary for subsequent test runs. You must copy the ID form the CLI or from the dashboard and pass it when running the test:

```bash
maestro cloud \
  --api-key <YOUR_API_KEY> \
  --project-id <YOUR_PROJECT_ID> \
  --app-binary-id <BINARY_ID> \
  .maestro/
```

This tells Maestro to skip the binary re-upload and go straight to execution.

#### Named parameters

While Maestro supports positional parameters for quick commands, using named parameters is strongly recommended for clarity and reliability, especially in CI/CD pipelines.

Named parameters such as `--app-file` and `--flows` can be provided in any order, making scripts easier to read and less error-prone.

<table><thead><tr><th width="259">Parameter</th><th>Purpose</th></tr></thead><tbody><tr><td><code>--app-file</code></td><td>Specifies the local app file path you are uploading.</td></tr><tr><td><code>--flows</code></td><td>Specifies the local directory or specific file of flows to test.</td></tr></tbody></table>

```bash
# Using a folder of flows
maestro cloud \
  --app-file app.apk \
  --flows myFlows/

# Using a single flow file
maestro cloud \
  --app-file app.apk \
  --flows flow.yaml
```

Because named parameters are explicit, their order does not matter:

```bash
# Order A
maestro cloud --app-file example.apk --flows ./myTests

# Order B
maestro cloud --flows ./myTests --app-file example.apk
```

If you rely on positional parameters, the order must be correct or the command will fail:

```bash
# This works
maestro cloud example.apk ./myTests

# This will FAIL
maestro cloud ./myTests example.apk
```

For CI environments and long-lived scripts, prefer named parameters to avoid subtle errors.

### Security

Reusing an app binary is a performance optimization and does not compromise security.

* **Access**: Only you or authorized members of your project can access the binary from your previous uploads.
* **Privacy**: All cloud devices are wiped after every test execution. Even after the test completes, no one, including the Maestro team, has access to the running application data.

### Related content

* [Maestro CLI reference](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/maestro-cli-commands-and-options): Full list of all available parameters.
