# Pull Request Integration

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

Robin also provides support for native pull request integration. This is useful if you'd like to run your Flows asynchronously but still block pull requests from landing if flow failures are detected.

{% hint style="info" %}
Maestro Cloud currently supports **Pull Request Integration** for GitHub and GitHub Enterprise only.

* ✅ GitHub Support
* ✅ GitHub Enterprise Support

Note that you can trigger [automatic uploads from **any CI platform**](ci-integration/).
{% endhint %}

### 1. Trigger uploads on every pull request

{% tabs %}
{% tab title="GitHub Actions" %}
1. Follow the steps described [here](pull-request-integration.md#github-actions)
2. Ensure your workflow is triggered on every pull request made against your Baseline Branch.

{% code lineNumbers="true" %}
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
1. Ensure that uploads to Maestro Cloud are triggered on every pull request. Exactly how this is accomplished depends on your CI setup.
2. Add the following options to your `maestro cloud` command:

```
maestro cloud \
  --async \
  --apiKey <apiKey> \
  --branch <branch> \
  --repoOwner <repoOwner> \
  --repoName <repoName> \
  --pullRequestId <pullRequestId> \
  --commitSha <commitSha> \
  <appFile> .maestro/

```

<table data-header-hidden><thead><tr><th width="164"></th><th></th></tr></thead><tbody><tr><td><strong>branch</strong></td><td>Set to the name of the git branch the app was built on and the pull request is based on (i.e. feature-foo)</td></tr><tr><td><strong>repoOwner</strong></td><td>Set to the owner of the repository (i.e. "mobile-dev-inc")</td></tr><tr><td><strong>repoName</strong></td><td>Set to the name of the repository (i.e. "fenix")</td></tr><tr><td><strong>pullRequestId</strong></td><td>Set to the unique identifier of the pull request. Only set when triggered by a Pull Request. (i.e. 1234)</td></tr><tr><td><strong>commitSha</strong></td><td>Set to the commit hash. Only set when triggered by a Pull Request. (i.e. 586e1c690891d20568976c78f06fbec9b94a3b32)</td></tr></tbody></table>


{% endtab %}

{% tab title="API" %}
1. Ensure that uploads are triggered on every pull request. Exactly how this is accomplished depends on your CI setup.
2. Add the following values to the JSON data in the upload API request:

<table data-header-hidden><thead><tr><th width="188"></th><th></th></tr></thead><tbody><tr><td><strong>repoOwner</strong></td><td>Set to the owner of the repository (i.e. "mobile-dev-inc")</td></tr><tr><td><strong>repoName</strong></td><td>Set to the name of the repository (i.e. "fenix")</td></tr><tr><td><strong>branch</strong></td><td>Set to the name of the git branch the app was built on and the pull request is based on (i.e. feature-foo)</td></tr><tr><td><strong>pullRequestId</strong></td><td>Set to the unique identifier of the pull request. Only set when triggered by a pull request. (i.e. 1234)</td></tr><tr><td><strong>commitSha</strong></td><td>Set to the commit hash. Only set when triggered by a Pull Request. (i.e. 586e1c690891d20568976c78f06fbec9b94a3b32)</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### 2. Grant access to pull requests

In order to update the status of pull requests, you'll need to grant Robin permissions to do so.

* [Install the Maestro Cloud GitHub App](https://github.com/apps/maestro-cloud-app)

### 3. Test the integration

Lastly, open a pull request and ensure that the Maestro Cloud check shows up on your pull request.

{% tabs %}
{% tab title="GitHub / GitHub Enterprise" %}
<figure><img src="../.gitbook/assets/image (2).png" alt="Successful check on Github PR page"><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
