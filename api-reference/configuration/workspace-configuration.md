# Workspace configuration

The directory where all your Maestro-related configuration lives is a _Maestro workspace_ (or just _workspace_ for short).

## Maestro configuration

The following properties can be configured on the workspace as a whole as part of the workspace configuration. All settings are optional.

* `flows`: inclusion patterns regarding what Flows to include ([docs](../../cli/test-suites-and-reports.md#controlling-what-tests-to-include)).
* `includeTags`: list of tags to include on each run ([docs](../../cli/tags.md#global-tags)).
* `excludeTags`: list of tags to exclude on each run ([docs](../../cli/tags.md#global-tags)).
* `executionOrder`: the order to run sequential tests before running remaining tests ([docs](../../cli/test-suites-and-reports.md#sequential-execution)).
* `baselineBranch`: Which branch is your baseline. Useful when integrating with Pull Requests ([docs](https://docs.maestro.dev/cloud/pull-request-integration)). Cloud only.
* `notifications`: Who to notify after an Upload finishes processing ([docs](../../cloud/reference/email-notifications.md)). Cloud only. You might prefer the [Slack integration](../../cloud/reference/slack-notifications.md).

### Example

Below is an example Maestro workspace configuration file. Typically it's named `config.yaml` and placed in the `.maestro` directory in your project's root:

```yaml
flows:
  - "subFolder/*"
includeTags:
  - tagNameToInclude
excludeTags:
  - tagNameToExclude
executionOrder:
    continueOnFailure: false # default is true
    flowsOrder:
        - flowA
        - flowB
  
# Cloud only config options
baselineBranch: main
notifications:
  email:
    enabled: true
    recipients:
      - john@example.com
```

### Multiple Configs

It's possible to have multiple config files in a repository and specify them at execution time. For example, the default `config.yaml` could cover the tests typically run on the main branch, but an additional `pr-config.yaml` might cover the flows and tags used when running tests on each Pull Request.

```bash
maestro cloud --config ./pr-config.yaml ./flows
```

## Environment variables

<table data-view="cards"><thead><tr><th>Variable name</th><th>Description</th><th>Type</th><th>Default</th><th>Further reading</th></tr></thead><tbody><tr><td>MAESTRO_API_URL</td><td>The URL of the Maestro API to use. Probably only useful to Mobile Inc developers.</td><td>String</td><td>https://api.copilot.mobile.dev</td><td>-</td></tr><tr><td>MAESTRO_CLI_AI_KEY</td><td>Key for external AI service used in AI operations</td><td>String</td><td>-</td><td><a href="ai-configuration.md">Docs</a></td></tr><tr><td>MAESTRO_CLI_AI_MODEL</td><td>Model for external AI service used in AI operations. The prefix of the model decides which service to use. If none is specified, OpenAI will be used.</td><td>String</td><td><code>gpt-4o</code> for OpenAI, <code>claude-3-5-sonnet-20240620</code> for Claude</td><td>-</td></tr><tr><td>MAESTRO_CLI_ANALYSIS_NOTIFICATION_DISABLED</td><td>Disables the notification displayed on each run about AI analysis</td><td>Boolean</td><td>false</td><td>-</td></tr><tr><td>MAESTRO_CLI_LOG_PATTERN_CONSOLE</td><td>Sets the <a href="https://logback.qos.ch/manual/layouts.html">logback layout</a> for logging in the console</td><td>String</td><td><code>%highlight([%5level]) %msg%n</code></td><td>-</td></tr><tr><td>MAESTRO_CLI_LOG_PATTERN_FILE</td><td>Sets the <a href="https://logback.qos.ch/manual/layouts.html">logback layout</a> for logging in the log file</td><td>String</td><td><code>%d{HH:mm:ss.SSS} [%5level] %logger.%method: %msg%n</code></td><td><a href="https://docs.maestro.dev/troubleshooting/debug-output#maestro-logs">Docs</a></td></tr><tr><td>MAESTRO_CLI_NO_ANALYTICS</td><td>Disables Maestro analytics collection</td><td>Boolean</td><td>false</td><td>-</td></tr><tr><td>MAESTRO_CLOUD_API_KEY</td><td>The API key to use when communicating with the Maestro cloud platform</td><td>String</td><td>-</td><td><a href="../../cloud/run-maestro-tests-in-the-cloud.md">Docs</a></td></tr><tr><td>MAESTRO_CLOUD_API_URL</td><td>Like <code>MAESTRO_API_URL</code>but used for AI API requests</td><td>String</td><td>https://api.copilot.mobile.dev</td><td>-</td></tr><tr><td>MAESTRO_DISABLE_UPDATE_CHECK</td><td>Disable the check for newer Maestro versions when running the CLI</td><td>Boolean</td><td>false</td><td>-</td></tr><tr><td>MAESTRO_DRIVER_STARTUP_TIMEOUT</td><td>The maximum time to wait for a driver to start</td><td>Number</td><td>15000</td><td><a href="../../advanced/configuring-maestro-driver-timeout.md">Docs</a></td></tr><tr><td>MAESTRO_USE_GRAALJS</td><td>Use GraalJS instead of RhinoJS for JavaScript execution</td><td>Boolean</td><td>false</td><td><a href="../../advanced/javascript/graaljs-support.md">Docs</a></td></tr></tbody></table>

Any other environment variables prefixed with `MAESTRO_` will be available in your Flows as JavaScript variables. See [Accessing variables from the shell](../../advanced/parameters-and-constants.md#accessing-variables-from-the-shell) for more information.
