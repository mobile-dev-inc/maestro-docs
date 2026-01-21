# Workspace configuration

This page provides a technical reference for all properties you can set in the `config.yaml` file. The configuration is structured into Global, Execution, Platform-specific, and Cloud sections.

### Global workspace settings

These settings define the identity of your application and how Maestro discovers your Flow files.

<table data-header-hidden><thead><tr><th width="140.111083984375"></th><th></th></tr></thead><tbody><tr><td><strong>Key</strong></td><td><strong>Description</strong></td></tr><tr><td><code>appId</code></td><td>Required. The unique identifier for your app. Use the Bundle ID for iOS, Package Name for Android, or the starting URL for Web.</td></tr><tr><td><a href="https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-discovery-and-tags"><code>flows</code></a></td><td>Glob patterns defining which files to include in a test suite. Defaults to <code>*</code> (only YAML files in the root folder). Use <code>**</code> for recursive discovery.</td></tr><tr><td><code>env</code></td><td>Global key-value pairs accessible as variables (e.g., <code>${MY_VAR}</code>) within your Flows.</td></tr><tr><td><a href="https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts"><code>testOutputDir</code></a></td><td>Custom directory where screenshots, logs, and metadata are saved. Defaults to <code>~/.maestro/tests/</code>.</td></tr></tbody></table>

#### Execution & Filtering

Use these keys to control the order and selection of tests during a suite run.

| **Key**                                                                                                                        | **Description**                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| [`includeTags`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-discovery-and-tags)                   | Only executes Flows that contain at least one of these tags in their internal configuration.       |
| [`excludeTags`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-discovery-and-tags)                   | Skips any Flows that contain one or more of these tags.                                            |
| [`executionOrder`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/sequential-execution)                   | A nested object used to force a specific sequence of Flows.                                        |
| [`executionOrder.continueOnFailure`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/sequential-execution) | If `false`, Maestro stops the sequential execution immediately if a Flow fails. Default is `true`. |
| [`executionOrder.flowsOrder`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/sequential-execution)        | The ordered list of Flow names or filenames (without `.yaml`) to execute sequentially.             |

#### Platform Configuration

Platform-specific settings allow you to optimize the environment for Android or iOS.

| **Key (iOS specifics)**      | **Description**                                                                                                                            |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `disableAnimations`          | Enables Reduce Motion on the iOS Simulator to prevent flakiness caused by system-level animations.                                         |
| `snapshotKeyHonorModalViews` | If `false`, Maestro includes elements from the background hierarchy even when a modal is present. Useful for certain custom UI frameworks. |

| **Key (Android specifics)** | **Description**                                                                            |
| --------------------------- | ------------------------------------------------------------------------------------------ |
| `disableAnimations`         | Disables system-level window, transition, and animator animations on the Android Emulator. |

#### Maestro Cloud Configuration

These properties are used only when running tests on [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/).

| **Key**                          | **Description**                                                                             |
| -------------------------------- | ------------------------------------------------------------------------------------------- |
| `baselineBranch`                 | Defines the source-of-truth branch (e.g., `main`) for visual regression and PR comparisons. |
| `notifications`                  | Configures automated alerts upon test completion.                                           |
| `notifications.email.enabled`    | Set to `true` to enable email notifications.                                                |
| `notifications.email.recipients` | A list of email addresses to receive the test reports.                                      |
| `notifications.slack.endpoint`   | The Webhook URL for posting results directly to a Slack channel.                            |
