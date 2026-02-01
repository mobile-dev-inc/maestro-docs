# Maestro CLI commands and options

This document lists all the options and subcommands you can pass to the Maestro CLI.

## Usage

To use the subcommands and/or options with the Maestro CLI, follow this pattern:

```bash
maestro -option -subcommand
```

## Options

You can pass these options with the Maestro CLI:

<table><thead><tr><th width="269.888916015625">Flag</th><th>Description</th></tr></thead><tbody><tr><td><code>-h</code>, <code>--help</code></td><td>Disply de help message for the flag or subcommand.</td></tr><tr><td><code>--[(no) ansi]</code>, <code>--[(no) color]</code></td><td>Enable or disabe color and ansi output.</td></tr><tr><td><code>-p</code>, <code>--platform</code></td><td>Select the platform to run the test on. Usage: <code>--platform=ios</code>.</td></tr><tr><td><code>--udid</code>, <code>--device</code></td><td>Pass the device ID to run the test on. Usage: <code>--device=00008030-001C195E0E88002E</code>.</td></tr><tr><td><code>-v</code>, <code>--version</code></td><td>Display the version of the Maestro CLI you have installed.</td></tr><tr><td><code>--verbose</code></td><td>Enable verbose mode.</td></tr></tbody></table>

## Subcommands

You can pass these subcommands with the Maestro CLI:

<table><thead><tr><th width="174.3333740234375">subcommand</th><th>Description</th></tr></thead><tbody><tr><td><code>test</code></td><td>Test a flow or a selected set of flows on a local iOS Simulator or Android Emulator.</td></tr><tr><td><code>cloud</code></td><td>Upload your flows to Maestro Cloud.</td></tr><tr><td><code>record</code></td><td>Record your flows.</td></tr><tr><td><code>download-samples</code></td><td>Download sample flows and sample apps for running with the Maestro CLI.</td></tr><tr><td><code>login</code></td><td>Login into Maestro Cloud.</td></tr><tr><td><code>logout</code></td><td>Logout from Maestro Cloud.</td></tr><tr><td><code>bugreport</code></td><td>Send a bug report.</td></tr><tr><td><code>start-device</code></td><td>Start a iOS Simulator or a Android Emulator.</td></tr><tr><td><code>chat</code></td><td>Use Maestro GPT to help you with the apps and tests.</td></tr><tr><td><code>driver-setup</code></td><td>Setup Maestro drivers for your device. By now, it supports iOS real devices.</td></tr><tr><td><code>mcp</code></td><td>Start the Maestro Model Context Protocol, MCP.</td></tr></tbody></table>

## Subcommands options

Each subcommand of Maestro CLI will have a series of other options.

### `test`

<table><thead><tr><th width="304.33331298828125">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>&#x3C;flowFiles>...</code></td><td>One or more flow files or folders containing flow files.</td></tr><tr><td><code>--analyze</code></td><td>[Beta] Enhance the test output analysis with AI Insights.</td></tr><tr><td><code>--api-key=&#x3C;apiKey></code></td><td>[Beta] API key.</td></tr><tr><td><code>--api-url=&#x3C;apiUrl></code></td><td>[Beta] API base URL.</td></tr><tr><td><code>-c, --continuous</code></td><td>Run tests in continuous mode.</td></tr><tr><td><code>--config=&#x3C;configFile></code></td><td>Optional YAML configuration file for the workspace.</td></tr><tr><td><code>--debug-output=&#x3C;debugOutput></code></td><td>Configures the debug output in this path, instead of default.</td></tr><tr><td><code>-e, --env=&#x3C;String=String></code></td><td>Set environment variables.</td></tr><tr><td><code>--exclude-tags=&#x3C;excludeTags></code></td><td>List of tags that will remove the Flows containing the provided tags.</td></tr><tr><td><code>--flatten-debug-output</code></td><td>All file outputs from the test case are created in the folder without subfolders or timestamps for each run.</td></tr><tr><td><code>--format=&#x3C;format></code></td><td>Test report format (default=NOOP): JUNIT, HTML, NOOP.</td></tr><tr><td><code>--format=&#x3C;format></code></td><td>The test report format. Default is NOOP, which means no output is produced. You can use JUNIT, HTML, or NOOP. JUNIT is the Java Unit test format, HTML is a web report, and NOOP means no operation.</td></tr><tr><td><code>-h, --help</code></td><td>Display help message.</td></tr><tr><td><code>--headless</code></td><td>(Web only) Run the tests in headless mode.</td></tr><tr><td><code>--include-tags=&#x3C;includeTags></code></td><td>List of tags that will remove the Flows that does not have the provided tags.</td></tr><tr><td><code>--[no-]ansi</code>, <code>--[no-]color</code></td><td>Enable / disable colors and ansi output.</td></tr><tr><td><code>--output=&#x3C;output></code></td><td>Specify the output destination.</td></tr><tr><td><code>-s, --shards=&#x3C;count></code></td><td>Number of parallel shards to distribute tests across.</td></tr><tr><td><code>--shard-all=&#x3C;shardAll></code></td><td>Run all the tests across N connected devices.</td></tr><tr><td><code>--shard-split=&#x3C;shardSplit></code></td><td>Run the tests across N connected devices, splitting the tests evenly across them.</td></tr><tr><td><code>--test-output-dir=&#x3C;testOutputDir></code></td><td>Configures the test output directory for screenshots and other test artifacts.</td></tr><tr><td><code>--test-suite-name=&#x3C;testSuiteName></code></td><td>Test suite name.</td></tr></tbody></table>

### `cloud`

| Option                                    | Description                                                                                                                                             |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--android-api-level=<level>`             | Android API level to run your flow against.                                                                                                             |
| `--apiKey, --api-key=<key>`               | API key for Maestro Cloud.                                                                                                                              |
| `--apiUrl, --api-url=<url>`               | API base URL.                                                                                                                                           |
| `--app-file=<path>`                       | App binary to run your Flows against.                                                                                                                   |
| `--appBinaryId, --app-binary-id=<id>`     | The ID of an app binary previously uploaded to Maestro Cloud.                                                                                           |
| `--async`                                 | Run the upload asynchronously and exit immediately.                                                                                                     |
| `--branch=<name>`                         | The branch this upload originated from.                                                                                                                 |
| `--commitSha, --commit-sha=<sha>`         | The commit SHA of this upload.                                                                                                                          |
| `--commitSha, --commit-sha=<sha>`         | Use the commit SHA (Secure Hash Algorithm) for this upload.                                                                                             |
| `--config=<file>`                         | Optional .yaml configuration file for Flows.                                                                                                            |
| `--device-locale=<locale>`                | Locale for the device (for example, "de\_DE" for Germany).                                                                                              |
| `--device-model=<model>`                  | iOS device model to run against (for example, iPhone-11).                                                                                               |
| `--device-os=<os>`                        | iOS version to run against (for example, iOS-17-5, iOS-18-2).                                                                                           |
| `-e, --env=<Key=Value>`                   | Environment variables to inject into your Flows.                                                                                                        |
| `--exclude-tags=<tags>`                   | List of tags that will remove the Flows containing the provided tags.                                                                                   |
| `--flows=<path>`                          | A Flow path or a folder path that contains Flows.                                                                                                       |
| `--format=<format>`                       | Test report format (default is NOOP, which means no output is produced): JUNIT (Java Unit), HTML, or NOOP (no operation).                               |
| `-h, --help`                              | Display help message.                                                                                                                                   |
| `--include-tags=<tags>`                   | List of tags that will remove the Flows that don't have the provided tags.                                                                              |
| `--ios-version=<version>`                 | iOS version. Deprecated: use `--device-os` instead.                                                                                                     |
| `--mapping=<path>`                        | dSYM file for iOS or Proguard mapping file for Android.                                                                                                 |
| `--name=<name>`                           | Name of the upload.                                                                                                                                     |
| `--[no-]ansi, --[no-]color`               | Enable / disable colors and ansi output.                                                                                                                |
| `--[no-]ansi, --[no-]color`               | Enable or turn off colors and ANSI output. ANSI stands for American National Standards Institute.                                                       |
| `--device-locale=<locale>`                | Set the device locale, for example: "de\_DE" for Germany. Use ISO-639-1 and ISO-3166-1 codes. ISO means International Organization for Standardization. |
| `chat`                                    | Use Maestro GPT, the Generative Pre-trained Transformer, to help you with the apps and tests.                                                           |
| `mcp`                                     | Start the Maestro Model Context Protocol, also known as MCP.                                                                                            |
| `--headless`                              | Run the tests in headless mode for web only.                                                                                                            |
| `--output=<path>`                         | File to write report into (default is report.xml).                                                                                                      |
| `--projectId, --project-id=<id>`          | Project ID.                                                                                                                                             |
| `--pullRequestId, --pull-request-id=<id>` | The ID of the pull request this upload originated from.                                                                                                 |
| `--repoName, --repo-name=<name>`          | Repository name (for example, GitHub repo slug).                                                                                                        |
| `--repoOwner, --repo-owner=<owner>`       | Repository owner (for example, GitHub organization or user slug).                                                                                       |
| `--test-suite-name=<name>`                | Test suite name.                                                                                                                                        |

### `record`

<table><thead><tr><th width="304.33331298828125">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>&#x3C;flowFile></code></td><td>The Flow file to record.</td></tr><tr><td><code>[&#x3C;outputFile>]</code></td><td>Output file for the rendered video. Only valid for local rendering using <code>--local</code>.</td></tr><tr><td><code>[&#x3C;outputFile>]</code></td><td>Save the rendered video to this output file. Only works with local rendering using <code>--local</code>.</td></tr><tr><td><code>--apple-team-id=&#x3C;appleTeamId></code></td><td>The unique 10-character Apple Team ID assigned to your team's account.</td></tr><tr><td><code>--config=&#x3C;configFile></code></td><td>Optional .yaml configuration file. Defaults to <code>config.yaml</code> in the root directory.</td></tr><tr><td><code>--debug-output=&#x3C;debugOutput></code></td><td>Configures a custom path for debug output.</td></tr><tr><td><code>-e, --env=&#x3C;String=String></code></td><td>Environment variables to inject into the Flow.</td></tr><tr><td><code>-h, --help</code></td><td>Display the help message.</td></tr><tr><td><code>--local</code></td><td>Beta: Record using local rendering. This becomes the default in a future release.</td></tr><tr><td><code>--local</code></td><td>Record using local rendering. This is a beta feature and will become the default in a future release.</td></tr><tr><td><code>--output=&#x3C;path></code></td><td>Write the report to this file. The default is report.xml.</td></tr><tr><td><code>--repoName, --repo-name=&#x3C;name></code></td><td>Set the repository name, for example: GitHub repo slug.</td></tr><tr><td><code>--repoOwner, --repo-owner=&#x3C;owner></code></td><td>Set the repository owner, for example: GitHub organization or user slug.</td></tr><tr><td><code>--[no-]ansi, --[no-]color</code></td><td>Enable or turn off colors and ANSI (American National Standards Institute) output in the terminal.</td></tr></tbody></table>

### `start-device`

<table><thead><tr><th width="224.33331298828125">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>--device-locale=&#x3C;locale></code></td><td>Combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code (for example, "de_DE" for Germany).</td></tr><tr><td><code>--device-locale=&#x3C;locale></code></td><td>Use a combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code, for example: "de_DE" for Germany.</td></tr><tr><td><code>--force-create</code></td><td>Overrides the existing device if it already exists.</td></tr><tr><td><code>-h, --help</code></td><td>Display the help message.</td></tr><tr><td><code>--os-version=&#x3C;version></code></td><td>OS version to use. iOS: 16, 17, 18. Android: 28, 29, 30, 31, 33.</td></tr><tr><td><code>--platform=&#x3C;platform></code></td><td>Platforms: <code>android</code> or <code>ios</code>.</td></tr></tbody></table>

{% hint style="warning" %}
Some options will be required to run yout tests, like th `<FlowFile>` and the `--parameter` options.
{% endhint %}
