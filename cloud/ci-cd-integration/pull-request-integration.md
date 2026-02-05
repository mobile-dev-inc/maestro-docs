---
description: >-
  Native pull request integration runs Maestro tests asynchronously and blocks
  merges on failures. Supports GitHub Enterprise.
---

# Pull request integration

Native pull request integration allows you to run Maestro Flows asynchronously on every code change. You can configure it to block pull requests from being merged if test failures are detected.

{% hint style="info" %}
**Maestro Cloud Plan required.** Pull request integration is available on the [Maestro Cloud Plan](https://signin.maestro.dev/sign-up).
{% endhint %}

{% hint style="info" %}
Maestro Cloud currently supports native pull request integration for:

* **GitHub**&#x20;
* **GitHub Enterprise** only.
{% endhint %}

{% stepper %}
{% step %}
### Trigger uploads on every pull request

You must configure your CI environment to trigger a Maestro Cloud upload for every pull request. You can accomplish this by using one of the following options:

{% tabs %}
{% tab title="GitHub Actions" %}
Trigger your workflow on `pull_request` events against your baseline branch.

{% code title="" %}
```yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```
{% endcode %}
{% endtab %}

{% tab title="Maestro CLI" %}
Add the `--async` flag and PR-specific metadata to your `maestro cloud` command.

```bash
maestro cloud \
  --async \
  --api-key <YOUR_API_KEY> \
  --branch <BRANCH_NAME> \
  --repo-owner <REPO_OWNER> \
  --repo-name <REPO_NAME> \
  --pull-request-id <PR_ID> \
  --commit-sha <COMMIT_SHA> \
  <APP_FILE> .maestro/
```

The following table describes each one of the required flags you must inform.

| Argument            | Description                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `--branch`          | The name of the git branch being tested (e.g., `feature-branch`). Maestro uses this to group results by branch in the console. |
| `--repo-owner`      | The owner (individual or organization) of the repository on GitHub. Required for posting status checks.                        |
| `--repo-name`       | The name of the repository. Combined with `--repo-owner`, this identifies the target project for integration.                  |
| `--pull-request-id` | The number of the pull request. Essential for linking the test run to a specific PR and enabling automated comments.           |
| `--commit-sha`      | The full 40-character SHA of the commit. This ensures test results are associated with the exact state of the code.            |
{% endtab %}

{% tab title="API" %}
If using the upload API directly, include the following fields in the JSON payload:

* `branch`
* `repoOwner`
* `repoName`
* `pullRequestId`
* `commitSha`

The following table describes each one of the required fields you must inform.

| Field           | Description                                                                                                                    |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `branch`        | The name of the git branch being tested (e.g., `feature-branch`). Maestro uses this to group results by branch in the console. |
| `repoOwner`     | The owner (individual or organization) of the repository on GitHub. Required for posting status checks.                        |
| `repoName`      | The name of the repository. Combined with `--repo-owner`, this identifies the target project for integration.                  |
| `pullRequestId` | The number of the pull request. Essential for linking the test run to a specific PR and enabling automated comments.           |
| `commitSha`     | The full 40-character SHA of the commit. This ensures test results are associated with the exact state of the code.            |
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
### Grant access to pull requests

Maestro requires permission to update pull request statuses. To accomplish this, you must install the [Maestro Cloud app](https://github.com/apps/maestro-cloud-app) and grant access to your repositories to the desired repositories.
{% endstep %}

{% step %}
### Test the integration&#xD;

Once configured, open a pull request. The Maestro Cloud status check appears in the checks section. A passing check indicates all Flows ran successfully, while a failing check indicates that at least one Flow failed.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}



