# Reuse app binary

To run multiple test scenarios on the same build, you can reuse a previously uploaded binary instead of re-uploading the same file. This optimization saves time and bandwidth.

{% hint style="info" %}
**Maestro Cloud Plan required** App binary reuse is available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Find the app binary ID

When you upload an app to Maestro Cloud, a unique app binary ID is generated. You can find this ID in two locations:

* **CLI output**: The ID is returned in the terminal response after a successful upload.

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
  <FLOW_OR_FOLDER>
```

By providing the `--app-binary-id`, Maestro will skip the binary upload. &#x20;

#### Optimize with `--app-file` and `--flows`

You can also explicitly specify the app file and flows via arguments for better clarity using `--app-file` and `--flows`

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

### Security

Reusing an app binary is a performance optimization and does not compromise security.

* **Access**: Only you or authorized members of your project can access the binary from your previous uploads.
* **Privacy**: All cloud devices are wiped after every test execution. Even after the test completes, no one, including the Maestro team, has access to the running application data.
