# Cloud Workspace Configuration

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

A workspace is a directory containing all your Flows and config.yaml. The workspace is usually named `.maestro` which is the recommendation, but you can name it whatever you like and pass it in when testing in the cloud either via CI or using the CLI.&#x20;

In `config.yaml`, there are two types of configurations you can make:&#x20;

* Maestro configuration (eg when running locally or in your own CI)
* Cloud configuration (configuration that applies when [running Flows in the cloud](../run-maestro-tests-in-the-cloud.md))

Below is an exhaustive list of configuration options that you can set in `config.yaml` to control execution in Maestro Cloud.

For an exhaustive list of Maestro configuration that impacts local running, please refer to the general [Workspace Configuration docs](../../api-reference/configuration/workspace-configuration.md).

{% hint style="info" %}
`flows`, `includeTags` and`excludeTags`are used **both** when running locally and in the cloud.
{% endhint %}

<table><thead><tr><th width="219">Config</th><th width="321">Use</th><th>Optional</th><th>Docs</th></tr></thead><tbody><tr><td><code>flows</code></td><td>Controls what Flows to include when running the workspace.</td><td>Yes</td><td><a href="../../cli/test-suites-and-reports.md#controlling-what-tests-to-include">Docs</a></td></tr><tr><td><code>includeTags</code></td><td>List of tags to include on each run.</td><td>Yes</td><td><a href="../../cli/tags.md#global-tags">Docs</a></td></tr><tr><td><code>excludeTags</code></td><td>List of tags to exclude on each run.</td><td>Yes</td><td><a href="../../cli/tags.md#global-tags">Docs</a></td></tr><tr><td><code>baselineBranch</code></td><td>Information about what branch is your baseline. Useful when integrating with Pull Requests.</td><td>Yes</td><td><a href="../pull-request-integration.md">Docs</a></td></tr><tr><td><code>notifications</code></td><td>Who to notify after an Upload finishes processing.</td><td>Yes</td><td><a href="email-notifications.md">Email</a> <a href="slack-notifications.md">Slack</a></td></tr><tr><td><code>executionOrder</code></td><td>What Flows to run in sequential order (if desired).</td><td>Yes</td><td><a href="execution-order.md">Link</a></td></tr></tbody></table>

```yaml
# .maestro/config.yaml

# Generic Maestro configuration
flows:
  - "subFolder/*"
includeTags:
  - tagNameToInclude
excludeTags:
  - tagNameToExclude

# Cloud only configuration
baselineBranch: main
notifications:
  email:
    enabled: true
    recipients:
      - john@something.com
executionOrder:
    continueOnFailure: false # default is true
    flowsOrder:
        - flowA
        - flowB
```
