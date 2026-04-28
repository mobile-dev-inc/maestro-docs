---
description: >-
  Complete reference for Maestro CLI global options and subcommands including
  test, cloud, record, start-device, and their specific options.
---

# Maestro CLI commands and options

This document lists all the options and subcommands you can pass to the Maestro CLI.

### Usage

To use the subcommands and/or options with the Maestro CLI, follow this pattern:

```bash
maestro [options] [subcommand] [subcommand options]
```

For example, to run a test with verbose logging and a specific tag:

```bash
 maestro --verbose test my-flow.yaml --include-tags=smoke
```

### Options

You can pass these global options with the Maestro CLI:

| Flag                          | Description                                                                         |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| `--[no-]ansi`, `--[no-]color` | Enable or disable color and ANSI output.                                            |
| `--udid`, `--device`          | Pass the device ID to run the test on. Usage: `--device=00008030-001C195E0E88002E`. |
| `-h`, `--help`                | Display the help message for the flag or subcommand.                                |
| `-p`, `--platform`            | Select the platform to run the test on. Usage: `--platform=ios`.                    |
| `--verbose`                   | Enable verbose mode.                                                                |
| `-v`, `--version`             | Display the version of the Maestro CLI you have installed.                          |

### Subcommands

You can pass these subcommands with the Maestro CLI:

| Subcommand         | Description                                                                          |
| ------------------ | ------------------------------------------------------------------------------------ |
| `bugreport`        | Send a bug report.                                                                   |
| `chat`             | Use Maestro GPT to help you with the apps and tests.                                 |
| `cloud`            | Upload your Flows to Maestro Cloud.                                                  |
| `download-samples`    | Download sample Flows and sample apps for running with the Maestro CLI.              |
| `driver-setup`        | Setup Maestro drivers for your device.                                               |
| `list-cloud-devices`  | List devices available on Maestro Cloud, grouped by platform.                        |
| `list-devices`        | List local devices available, grouped by platform.                                   |
| `login`               | Login into Maestro Cloud.                                                            |
| `logout`              | Logout from Maestro Cloud.                                                           |
| `mcp`                 | Start the Maestro Model Context Protocol (MCP).                                      |
| `record`              | Record your Flows.                                                                   |
| `start-device`        | Start an iOS Simulator or an Android Emulator.                                       |
| `test`                | Test a Flow or a selected set of Flows on a local iOS Simulator or Android Emulator. |

### Subcommand Options

Each subcommand of Maestro CLI supports specific options.

#### `test`

Run tests on your local device or emulator.

| Option                              | Description                                                                                                  |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `--analyze`                         | \[Beta] Enhance the test output analysis with AI Insights.                                                   |
| `--api-key=<apiKey>`                | \[Beta] API key.                                                                                             |
| `--api-url=<apiUrl>`                | \[Beta] API base URL.                                                                                        |
| `--[no-]ansi`, `--[no-]color`       | Enable / disable colors and ANSI output.                                                                     |
| `--config=<configFile>`             | Optional YAML configuration file for the workspace.                                                          |
| `-c`, `--continuous`                | Run tests in continuous mode.                                                                                |
| `--debug-output=<debugOutput>`      | Configures the debug output in this path, instead of default.                                                |
| `-e`, `--env=<String=String>`       | Set environment variables.                                                                                   |
| `--exclude-tags=<excludeTags>`      | List of tags that will remove the Flows containing the provided tags.                                        |
| `--flatten-debug-output`            | All file outputs from the test case are created in the folder without subfolders or timestamps for each run. |
| `--format=<format>`                 | Test report format (default=NOOP). Options: `JUNIT`, `HTML`, `NOOP`.                                         |
| `-h`, `--help`                      | Display help message.                                                                                        |
| `--headless`                        | (Web only) Run the tests in headless mode.                                                                   |
| `--include-tags=<includeTags>`      | List of tags. Only flows containing these tags will be run.                                                  |
| `--output=<output>`                 | Specify the output destination.                                                                              |
| `--screen-size=<width>x<height>`    | Specify the dimensions of the headless browser, e.g. 1920x1080. Web only.                                    |
| `-s`, `--shards=<count>`            | Number of parallel shards to distribute tests across.                                                        |
| `--shard-all=<shardAll>`            | Run all the tests across N connected devices.                                                                |
| `--shard-split=<shardSplit>`        | Run the tests across N connected devices, splitting the tests evenly across them.                            |
| `--test-output-dir=<testOutputDir>` | Configures the test output directory for screenshots and other test artifacts.                               |
| `--test-suite-name=<testSuiteName>` | Test suite name.                                                                                             |
| `<flowFiles>...`                    | One or more flow files or folders containing flow files.                                                     |

#### `cloud`

Upload and run your flows on Maestro Cloud.

| Option                                      | Description                                                           |
| ------------------------------------------- | --------------------------------------------------------------------- |
| `--android-api-level=<level>`               | (Deprecated) Android API level. Use `--device-os` instead.            |
| `--apiKey`, `--api-key=<key>`               | API key for Maestro Cloud.                                            |
| `--apiUrl`, `--api-url=<url>`               | API base URL.                                                         |
| `--appBinaryId`, `--app-binary-id=<id>`     | The ID of an app binary previously uploaded to Maestro Cloud.         |
| `--app-file=<path>`                         | App binary to run your Flows against.                                 |
| `--async`                                   | Run the upload asynchronously and exit immediately.                   |
| `--branch=<name>`                           | The branch this upload originated from.                               |
| `--commitSha`, `--commit-sha=<sha>`         | The commit SHA of this upload.                                        |
| `--config=<file>`                           | Optional .yaml configuration file for Flows.                          |
| `--device-locale=<locale>`                  | Locale for the device (e.g., "de\_DE" for Germany).                   |
| `--device-model=<model>`                    | Device model to run against. iOS: `iPhone-11`, `iPhone-17-Pro`, etc. Android: `pixel_6`, `pixel_7`, etc. Run `maestro list-cloud-devices` to see all supported models. |
| `--device-os=<os>`                          | OS version to run against. iOS: `iOS-18-2`, `iOS-26-2` etc. Android: `android-33`, `android-34`, etc. Run `maestro list-cloud-devices` to see all supported versions. |
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
| `--[no-]ansi`, `--[no-]color`         | Enable or turn off colors and ANSI output.                                          |
| `--config=<configFile>`               | Optional .yaml configuration file. Defaults to `config.yaml` in the root directory. |
| `--debug-output=<debugOutput>`        | Configures a custom path for debug output.                                          |
| `-e`, `--env=<String=String>`         | Environment variables to inject into the Flow.                                      |
| `-h`, `--help`                        | Display the help message.                                                           |
| `--local`                             | Record using local rendering (Beta).                                                |
| `--output=<path>`                     | Write the report to this file. The default is report.xml.                           |
| `--repoName`, `--repo-name=<name>`    | Set the repository name.                                                            |
| `--repoOwner`, `--repo-owner=<owner>` | Set the repository owner.                                                           |

#### `start-device`

Launch an emulator or simulator.

| Option                     | Description                                                                             |
| -------------------------- | --------------------------------------------------------------------------------------- |
| `--device-locale=<locale>` | Combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code (e.g., "de\_DE"). |
| `--device-model=<model>`   | Device model to run against. iOS: `iPhone-11`, `iPhone-11-Pro`, etc. Android: `pixel_6`, `pixel_7`, etc. Run `maestro list-devices` to see all supported models. |
| `--device-os=<os>`         | OS version to use. iOS: `iOS-16-2`, `iOS-17-5`, `iOS-18-2`, etc. Android: `android-33`, `android-34`, etc. Run `maestro list-devices` to see all supported versions. |
| `--force-create`           | Overrides the existing device if it already exists.                                     |
| `-h`, `--help`             | Display the help message.                                                               |
| `--os-version=<version>`   | (Deprecated) OS version. Use `--device-os` instead.                                     |
| `--platform=<platform>`    | Platforms: `android`, `ios`, or `web`                                                   |

#### `list-devices`

List local devices available, grouped by platform.

| Option                     | Description                                          |
| -------------------------- | ---------------------------------------------------- |
| `-h`, `--help`             | Display the help message.                            |
| `--platform=<platform>`    | Filter by platform: `android`, `ios`, or `web`.      |

#### `list-cloud-devices`

List devices available on Maestro Cloud, grouped by platform.

| Option                     | Description                                          |
| -------------------------- | ---------------------------------------------------- |
| `-h`, `--help`             | Display the help message.                            |
| `--platform=<platform>`    | Filter by platform: `android`, `ios`, or `web`.      |

### Named parameters

While Maestro supports positional parameters for quick commands, using named parameters is strongly recommended for clarity and reliability, especially in CI/CD pipelines.

Named parameters such as `--app-file` and `--flows` can be provided in any order, making scripts easier to read and less error-prone.

| Parameter    | Purpose                                                          |
| ------------ | ---------------------------------------------------------------- |
| `--app-file` | Specifies the local app file path you are uploading.             |
| `--flows`    | Specifies the local directory or specific file of flows to test. |

```bash
# Using a folder of flows
maestro cloud \
  --app-file app.apk \
  --flows myFlows/

# Using a single flow file
maestro cloud \
  --app-file app.apk \
  --flows flow.yaml
```

Because named parameters are explicit, their order does not matter:

```bash
# Order A
maestro cloud --app-file example.apk --flows ./myTests

# Order B
maestro cloud --flows ./myTests --app-file example.apk
```

If you rely on positional parameters, the order must be correct or the command will fail:

```bash
# This works
maestro cloud example.apk ./myTests

# This will FAIL
maestro cloud ./myTests example.apk
```

For CI environments and long-lived scripts, prefer named parameters to avoid subtle errors.
