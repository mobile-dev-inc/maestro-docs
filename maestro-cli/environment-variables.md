---
description: >-
  Reference for all environment variables supported by the Maestro CLI,
  covering   logging, analytics, cloud authentication, and driver behavior.
---

# Environment variables

You can configure the Maestro CLI behavior using the following environment variables. Set them in your shell or CI/CD environment before running any `maestro` command.

| Variable                                     | Type    | Default                                              | Description                                                                                                                                                                                                                                                                     |
| -------------------------------------------- | ------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `MAESTRO_CLI_ANALYSIS_NOTIFICATION_DISABLED` | Boolean | `false`                                              | Disables the notification displayed on each run about AI analysis.                                                                                                                                                                                                              |
| `MAESTRO_CLI_LOG_PATTERN_CONSOLE`            | String  | `%highlight([%5level]) %msg%n`                       | Controls the console logging format using [Logback layout](https://logback.qos.ch/manual/layouts.html) patterns.                                                                                                                                                                |
| `MAESTRO_CLI_LOG_PATTERN_FILE`               | String  | `%d{HH:mm:ss.SSS} [%5level] %logger.%method: %msg%n` | Controls the file logging format using [Logback layout](https://logback.qos.ch/manual/layouts.html) patterns. For more information, see [Test reports and artifacts](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts "mention"). |
| `MAESTRO_CLI_NO_ANALYTICS`                   | Boolean | `false`                                              | Disables Maestro analytics collection.                                                                                                                                                                                                                                          |
| `MAESTRO_CLOUD_API_KEY`                      | String  | Not set                                              | The API key used when communicating with Maestro Cloud. Required for cloud operations. For more information, see [Run tests on Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/run-tests-on-maestro-cloud "mention").                                             |
| `MAESTRO_DISABLE_UPDATE_CHECK`               | Boolean | `false`                                              | Disables the check for newer Maestro versions when running the CLI.                                                                                                                                                                                                             |
| `MAESTRO_DRIVER_STARTUP_TIMEOUT`             | Number  | `15000`                                              | The maximum time (in milliseconds) to wait for a driver to start. For more information, see [run-your-first-test-with-the-maestro-cli.md](run-your-first-test-with-the-maestro-cli.md "mention").                                                                               |

#### Usage examples

{% tabs %}
{% tab title="Disable analytics" %}
```shellscript
export MAESTRO_CLI_NO_ANALYTICS=true
export MAESTRO_CLI_ANALYSIS_NOTIFICATION_DISABLED=true
maestro test my-flow.yaml
```
{% endtab %}

{% tab title="Cloud authentication" %}
```shellscript
export MAESTRO_CLOUD_API_KEY=your_api_key_here
maestro cloud --app-file app.apk --flows ./flows
```
{% endtab %}

{% tab title="Driver startup timeout" %}
```shellscript
export MAESTRO_DRIVER_STARTUP_TIMEOUT=30000
maestro test my-flow.yaml
```
{% endtab %}

{% tab title="Custom log format" %}
```shellscript
export MAESTRO_CLI_LOG_PATTERN_CONSOLE="%d{HH:mm:ss} [%level] %msg%n"
maestro test my-flow.yaml
```
{% endtab %}
{% endtabs %}
