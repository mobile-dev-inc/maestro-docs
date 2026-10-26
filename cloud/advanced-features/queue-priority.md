---
description: >-
  Set an upload's queue priority so its flows start before other flows your
  organization has waiting in the queue.
---

# Queue priority

When your organization has more flows queued than it can run at once, Maestro Cloud starts them in the order they were submitted. Queue priority lets you change that order: give an upload `high` priority and its flows start before your organization's `normal` and `low` priority flows that are still waiting.

Every upload has one of three priorities:

| Priority | Use it for                                                              |
| -------- | ----------------------------------------------------------------------- |
| `high`   | Uploads that need results first, such as a release candidate or hotfix. |
| `normal` | Everything else. This is the default.                                   |
| `low`    | Uploads that can wait, such as nightly or exploratory runs.             |

{% hint style="info" %}
Setting the priority from CI or the MCP requires Maestro CLI 2.12.0 or later.
{% endhint %}

### How it works

* Priority only reorders flows **within your organization**. It never moves your flows ahead of another organization's, and it doesn't change your concurrency limits.
* Flows with the same priority start in the order they were submitted.
* Priority is strict. While `high` priority flows for a platform are ready to start, your `normal` and `low` priority flows on that platform wait.
* Flows that are already running are not interrupted.
* A retried flow runs at the upload's current priority and joins the back of that priority's queue.

### Set the priority when you upload

{% tabs %}
{% tab title="Maestro CLI" %}
Pass `--priority`:

```bash
maestro cloud \
  --api-key <YOUR_API_KEY> \
  --project-id <YOUR_PROJECT_ID> \
  --app-file <APP_FILE> \
  --priority high \
  --flows .maestro/
```
{% endtab %}

{% tab title="GitHub Actions" %}
Set the `priority` input:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v3
  with:
    api-key: ${{ secrets.MAESTRO_API_KEY }}
    project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
    app-file: app/build/outputs/apk/debug/app-debug.apk
    priority: high
```
{% endtab %}

{% tab title="Bitrise" %}
Set the `priority` input on the **Maestro Cloud Upload** step:

```yaml
- maestro-cloud-upload@1:
    inputs:
    - api_key: $CLOUD_API_KEY
    - project_id: $MAESTRO_PROJECT_ID
    - app_file: $BITRISE_APK_PATH
    - priority: high
```
{% endtab %}

{% tab title="Bitbucket Pipelines" %}
Set `MDEV_PRIORITY` on the Maestro Cloud Upload pipe:

```yaml
- pipe: mobiledevinc/maestro-cloud-upload:1.8.0
  variables:
    MDEV_API_KEY: $MDEV_API_KEY
    MDEV_PROJECT_ID: $MDEV_PROJECT_ID
    MDEV_APP_FILE: app-release.apk
    MDEV_PRIORITY: high
```
{% endtab %}

{% tab title="MCP" %}
Pass `priority` to the `run_on_cloud` tool. Your agent will do this when you ask for it, for example "run these flows on Maestro Cloud with high priority".
{% endtab %}
{% endtabs %}

The value is case-insensitive. Any value other than `low`, `normal` or `high` is rejected and the upload doesn't start.

### Change the priority of an upload

You can change the priority of an upload while it still has flows that haven't finished, for example to move a waiting upload ahead of the rest.

1. Open the upload in the Maestro Console, or find it in its app's list of uploads.
2. Click the priority badge, next to **Queue Priority** on the upload page or on the upload's row in the list.
3. Choose **Low**, **Normal** or **High**.

The new priority applies to the upload's flows that haven't finished yet, and to any later retries. Changing the priority doesn't reset how long a flow has been queued.

### Next steps

* Read [automatic-retries.md](automatic-retries.md "mention") to see when Maestro Cloud retries a flow for you.
* Use [stop-previous-flows.md](stop-previous-flows.md "mention") to cancel superseded uploads so they don't hold up the queue.
