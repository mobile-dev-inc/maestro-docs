---
description: >-
  Configure GitHub Action triggers and use output variables to integrate Maestro
  Cloud into your CI/CD pipeline.
---

# Outputs and triggers

To integrate Maestro Cloud seamlessly into your CI/CD pipeline, you need to configure when the action runs and how to use its results (e.g., posting a comment on a PR or failing a build).

### Triggers

You can trigger the Maestro Cloud action on various GitHub events. The most common are `push` and `pull_request`.

The following code snippet shows an example to trigger the action on pushes to your main branch and when pull requests are opened against it.

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
```

#### Supporting Forks (`pull_request_target`)

If your repository receives pull requests from forks (which do not have access to your secrets by default), you may need to use the `pull_request_target` trigger.

{% hint style="info" %}
When using `pull_request_target`, you should explicitly checkout the PR's HEAD commit to ensure you are testing the new code, not the base branch.
{% endhint %}

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

For more details on security and triggers, refer to [GitHub's documentation](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows).

### Action outputs

The Maestro Cloud action sets several output variables that you can use in subsequent steps of your workflow. To access them, you must give your step an `id`.

The following output variables are set by the action:

| **Output variable**           | **Description**                                                                          |
| ----------------------------- | ---------------------------------------------------------------------------------------- |
| `MAESTRO_CLOUD_CONSOLE_URL`   | The URL to view the test results in the Maestro Cloud Console.                           |
| `MAESTRO_CLOUD_APP_BINARY_ID` | The ID of the uploaded binary (useful for reusing the binary in later steps).            |
| `MAESTRO_CLOUD_UPLOAD_STATUS` | The final status of the upload. Not available in async mode.                             |
| `MAESTRO_CLOUD_FLOW_RESULTS`  | A JSON string containing the results of individual Flows. _Not available in async mode._ |

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

The `MAESTRO_CLOUD_UPLOAD_STATUS` output will contain one of the following strings:

* `PENDING`
* `PREPARING`
* `INSTALLING`
* `RUNNING`
* `SUCCESS`
* `ERROR`
* `CANCELED`
* `WARNING`
* `STOPPED`

Meanwhile, the `MAESTRO_CLOUD_FLOW_RESULTS` output is a JSON array containing objects with the following structure:

```json
[
  {
    "name": "my-first-flow",
    "status": "SUCCESS",
    "errors": []
  },
  {
    "name": "my-second-flow",
    "status": "SUCCESS",
    "errors": []
  },
  {
    "name": "my-cancelled-flow",
    "status": "CANCELED",
    "errors": [],
    "cancellationReason": "INFRA_ERROR"
  }
]
```

You can use a tool like `jq` in a subsequent step to parse this JSON and perform custom logic (e.g., sending a Slack notification with specific failure details).

### Related content

Learn how to send notifications after test finish using [Slack](../../notifications/set-slack-notification.md), [email](../../notifications/set-email-notification.md), or [webhooks](../../notifications/configure-webhooks.md).
