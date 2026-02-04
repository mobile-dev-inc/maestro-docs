---
description: >-
  Complete reference for all Maestro CLI commands, subcommands, and options
  including test, cloud, record, and start-device.
---

# Maestro CLI commands and options

This document lists all the options and subcommands you can pass to the Maestro CLI.

### Usage

To use the subcommands and/or options with the Maestro CLI, follow this pattern:

```bash
maestro [options] [subcommand]
```

### Options

You can pass these global options with the Maestro CLI:

| Flag                          | Description                                                                         |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| `-h`, `--help`                | Display the help message for the flag or subcommand.                                |
| `--[no-]ansi`, `--[no-]color` | Enable or disable color and ANSI output.                                            |
| `-p`, `--platform`            | Select the platform to run the test on. Usage: `--platform=ios`.                    |
| `--udid`, `--device`          | Pass the device ID to run the test on. Usage: `--device=00008030-001C195E0E88002E`. |
| `-v`, `--version`             | Display the version of the Maestro CLI you have installed.                          |
| `--verbose`                   | Enable verbose mode.                                                                |

### Subcommands

You can pass these subcommands with the Maestro CLI:

| Subcommand         | Description                                                                          |
| ------------------ | ------------------------------------------------------------------------------------ |
| `test`             | Test a flow or a selected set of flows on a local iOS Simulator or Android Emulator. |
| `cloud`            | Upload your flows to Maestro Cloud.                                                  |
| `record`           | Record your flows.                                                                   |
| `download-samples` | Download sample flows and sample apps for running with the Maestro CLI.              |
| `login`            | Login into Maestro Cloud.                                                            |
| `logout`           | Logout from Maestro Cloud.                                                           |
| `bugreport`        | Send a bug report.                                                                   |
| `start-device`     | Start an iOS Simulator or an Android Emulator.                                       |
| `chat`             | Use Maestro GPT to help you with the apps and tests.                                 |
| `driver-setup`     | Setup Maestro drivers for your device.                                               |
| `mcp`              | Start the Maestro Model Context Protocol (MCP).                                      |

### Subcommand Options

Each subcommand of Maestro CLI supports specific options.

#### `test`

Run tests on your local device or emulator.

| Option                              | Description                                                                                                  |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `<flowFiles>...`                    | One or more flow files or folders containing flow files.                                                     |
| `--analyze`                         | \[Beta] Enhance the test output analysis with AI Insights.                                                   |
| `--api-key=<apiKey>`                | \[Beta] API key.                                                                                             |
| `--api-url=<apiUrl>`                | \[Beta] API base URL.                                                                                        |
| `-c`, `--continuous`                | Run tests in continuous mode.                                                                                |
| `--config=<configFile>`             | Optional YAML configuration file for the workspace.                                                          |
| `--debug-output=<debugOutput>`      | Configures the debug output in this path, instead of default.                                                |
| `-e`, `--env=<String=String>`       | Set environment variables.                                                                                   |
| `--exclude-tags=<excludeTags>`      | List of tags that will remove the Flows containing the provided tags.                                        |
| `--flatten-debug-output`            | All file outputs from the test case are created in the folder without subfolders or timestamps for each run. |
| `--format=<format>`                 | Test report format (default=NOOP). Options: `JUNIT`, `HTML`, `NOOP`.                                         |
| `-h`, `--help`                      | Display help message.                                                                                        |
| `--headless`                        | (Web only) Run the tests in headless mode.                                                                   |
| `--include-tags=<includeTags>`      | List of tags. Only flows containing these tags will be run.                                                  |
| `--[no-]ansi`, `--[no-]color`       | Enable / disable colors and ANSI output.                                                                     |
| `--output=<output>`                 | Specify the output destination.                                                                              |
| `-s`, `--shards=<count>`            | Number of parallel shards to distribute tests across.                                                        |
| `--shard-all=<shardAll>`            | Run all the tests across N connected devices.                                                                |
| `--shard-split=<shardSplit>`        | Run the tests across N connected devices, splitting the tests evenly across them.                            |
| `--test-output-dir=<testOutputDir>` | Configures the test output directory for screenshots and other test artifacts.                               |
| `--test-suite-name=<testSuiteName>` | Test suite name.                                                                                             |

#### `cloud`

Upload and run your flows on Maestro Cloud.

| Option                                      | Description                                                           |
| ------------------------------------------- | --------------------------------------------------------------------- |
| `--android-api-level=<level>`               | Android API level to run your flow against.                           |
| `--apiKey`, `--api-key=<key>`               | API key for Maestro Cloud.                                            |
| `--apiUrl`, `--api-url=<url>`               | API base URL.                                                         |
| `--app-file=<path>`                         | App binary to run your Flows against.                                 |
| `--appBinaryId`, `--app-binary-id=<id>`     | The ID of an app binary previously uploaded to Maestro Cloud.         |
| `--async`                                   | Run the upload asynchronously and exit immediately.                   |
| `--branch=<name>`                           | The branch this upload originated from.                               |
| `--commitSha`, `--commit-sha=<sha>`         | The commit SHA of this upload.                                        |
| `--config=<file>`                           | Optional .yaml configuration file for Flows.                          |
| `--device-locale=<locale>`                  | Locale for the device (e.g., "de\_DE" for Germany).                   |
| `--device-model=<model>`                    | iOS device model to run against (e.g., iPhone-11).                    |
| `--device-os=<os>`                          | iOS version to run against (e.g., iOS-17-5, iOS-18-2).                |
| `-e`, `--env=<Key=Value>`                   | Environment variables to inject into your Flows.                      |
| `--exclude-tags=<tags>`                     | List of tags that will remove the Flows containing the provided tags. |
| `--flows=<path>`                            | A Flow path or a folder path that contains Flows.                     |
| `--format=<format>`                         | Test report format (default=NOOP). Options: `JUNIT`, `HTML`, `NOOP`.  |
| `-h`, `--help`                              | Display help message.                                                 |
| `--include-tags=<tags>`                     | List of tags. Only flows containing these tags will be run.           |
| `--ios-version=<version>`                   | (Deprecated) iOS version. Use `--device-os` instead.                  |
| `--mapping=<path>`                          | dSYM file for iOS or Proguard mapping file for Android.               |
| `--name=<name>`                             | Name of the upload.                                                   |
| `--[no-]ansi`, `--[no-]color`               | Enable / disable colors and ANSI output.                              |
| `--output=<path>`                           | File to write report into (default is report.xml).                    |
| `--projectId`, `--project-id=<id>`          | Project ID.                                                           |
| `--pullRequestId`, `--pull-request-id=<id>` | The ID of the pull request this upload originated from.               |
| `--repoName`, `--repo-name=<name>`          | Repository name (e.g., GitHub repo slug).                             |
| `--repoOwner`, `--repo-owner=<owner>`       | Repository owner (e.g., GitHub organization or user slug).            |
| `--test-suite-name=<name>`                  | Test suite name.                                                      |

#### `record`

Record your flow execution.

| Option                                | Description                                                                         |
| ------------------------------------- | ----------------------------------------------------------------------------------- |
| `<flowFile>`                          | The Flow file to record.                                                            |
| `[<outputFile>]`                      | Output file for the rendered video. Only valid for local rendering using `--local`. |
| `--apple-team-id=<appleTeamId>`       | The unique 10-character Apple Team ID assigned to your team's account.              |
| `--config=<configFile>`               | Optional .yaml configuration file. Defaults to `config.yaml` in the root directory. |
| `--debug-output=<debugOutput>`        | Configures a custom path for debug output.                                          |
| `-e`, `--env=<String=String>`         | Environment variables to inject into the Flow.                                      |
| `-h`, `--help`                        | Display the help message.                                                           |
| `--local`                             | Record using local rendering (Beta).                                                |
| `--output=<path>`                     | Write the report to this file. The default is report.xml.                           |
| `--repoName`, `--repo-name=<name>`    | Set the repository name.                                                            |
| `--repoOwner`, `--repo-owner=<owner>` | Set the repository owner.                                                           |
| `--[no-]ansi`, `--[no-]color`         | Enable or turn off colors and ANSI output.                                          |

#### `start-device`

Launch an emulator or simulator.

| Option                     | Description                                                                             |
| -------------------------- | --------------------------------------------------------------------------------------- |
| `--device-locale=<locale>` | Combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code (e.g., "de\_DE"). |
| `--force-create`           | Overrides the existing device if it already exists.                                     |
| `-h`, `--help`             | Display the help message.                                                               |
| `--os-version=<version>`   | OS version to use. iOS: 16, 17, 18. Android: 28, 29, 30, 31, 33.                        |
| `--platform=<platform>`    | Platforms: `android`, `ios`, or `web`                                                   |
