# Subcommands and options for Maestro CLI

This document lists all the options and subcommands you can pass to the Maestro CLI.

## Usage

To use the subcommands and/or options with the Maestro CLI, follow this pattern:

```bash
maestro -option -subcommand
```

## Options

You can pass these options with the Maestro CLI:

| Flag | Description | 
| --- | --- |
| `-h`, `--help` | Disply de help message for the flag or subcommand. |
| `--[(no) ansi]`, `--[(no) color]` | Enable or disabe color and ansi output. |
| `-p`, `--platform` | Select the platform to run the test on. Usage: `--platform=ios`. |
| `--udid`, `--device` | Pass the device ID to run the test on. Usage: `--device=00008030-001C195E0E88002E`. |
| `-v`, `--version` | Display the version of the Maestro CLI you have installed. |
| `--verbose` | Enable verbose mode. |

## Subcommands

You can pass these subcommands with the Maestro CLI:

| subcommand | Description |
| --- | --- |
| `test` | Test a flow or a selected set of flows on a local iOS Simulator or Android Emulator. | 
| `cloud` | Upload your flows to Maestro Cloud. |
| `record` | Record your flows. |
| `download-samples` | Download sample flows and sample apps for running with the Maestro CLI. |
| `login` | Login into Maestro Cloud. |
| `logout` | Logout from Maestro Cloud. |
| `bugreport` | Send a bug report. |
| `start-device` | Start a iOS Simulator or a Android Emulator. |
| `chat` | Use Maestro GPT to help you with the apps and tests. |
| `driver-setup` | Setup Maestro drivers for your device. By now, it supports iOS real devices. |
| `mcp` | Start the Maestro Model Context Protocol, MCP. |

## Subcommands options

Each subcommand of Maestro CLI will have a series of other options. 

### `test`

| Option | Description |
| --- | --- |
| `<flowFiles>...` | One or more flow files or folders containing flow files. |
| `--analyze` | [Beta] Enhance the test output analysis with AI Insights. |
| `--api-key=<apiKey>` | [Beta] API key. |
| `--api-url=<apiUrl>` | [Beta] API base URL. |
| `-c, --continuous` | Run tests in continuous mode. |
| `--config=<configFile>` | Optional YAML configuration file for the workspace. |
| `--debug-output=<debugOutput>` | Configures the debug output in this path, instead of default. |
| `-e, --env=<String=String>` | Set environment variables. |
| `--exclude-tags=<excludeTags>` | List of tags that will remove the Flows containing the provided tags. |
| `--flatten-debug-output` | All file outputs from the test case are created in the folder without subfolders or timestamps for each run. |
| `--format=<format>` | Test report format (default=NOOP): JUNIT, HTML, NOOP. |
| `--format=<format>` | The test report format. Default is NOOP, which means no output is produced. You can use JUNIT, HTML, or NOOP. JUNIT is the Java Unit test format, HTML is a web report, and NOOP means no operation. |
| `-h, --help` | Display help message. |
| `--headless` | (Web only) Run the tests in headless mode. |
| `--include-tags=<includeTags>` | List of tags that will remove the Flows that does not have the provided tags. |
| `--[no-]ansi`, `--[no-]color` | Enable / disable colors and ansi output. |
| `--output=<output>` | Specify the output destination. |
| `-s, --shards=<count>` | Number of parallel shards to distribute tests across. |
| `--shard-all=<shardAll>` | Run all the tests across N connected devices. |
| `--shard-split=<shardSplit>` | Run the tests across N connected devices, splitting the tests evenly across them. |
| `--test-output-dir=<testOutputDir>` | Configures the test output directory for screenshots and other test artifacts. |
| `--test-suite-name=<testSuiteName>` | Test suite name. |

### `cloud`

| Option | Description |
| --- | --- |
| `--android-api-level=<level>` | Android API level to run your flow against. |
| `--apiKey, --api-key=<key>` | API key for Maestro Cloud. |
| `--apiUrl, --api-url=<url>` | API base URL. |
| `--app-file=<path>` | App binary to run your Flows against. |
| `--appBinaryId, --app-binary-id=<id>` | The ID of an app binary previously uploaded to Maestro Cloud. |
| `--async` | Run the upload asynchronously and exit immediately. |
| `--branch=<name>` | The branch this upload originated from. |
| `--commitSha, --commit-sha=<sha>` | The commit SHA of this upload. |
| `--commitSha, --commit-sha=<sha>` | Use the commit SHA (Secure Hash Algorithm) for this upload. |
| `--config=<file>` | Optional .yaml configuration file for Flows. |
| `--device-locale=<locale>` | Locale for the device (for example, "de_DE" for Germany). |
| `--device-model=<model>` | iOS device model to run against (for example, iPhone-11). |
| `--device-os=<os>` | iOS version to run against (for example, iOS-17-5, iOS-18-2). |
| `-e, --env=<Key=Value>` | Environment variables to inject into your Flows. |
| `--exclude-tags=<tags>` | List of tags that will remove the Flows containing the provided tags. |
| `--flows=<path>` | A Flow path or a folder path that contains Flows. |
| `--format=<format>` | Test report format (default is NOOP, which means no output is produced): JUNIT (Java Unit), HTML, or NOOP (no operation). |
| `-h, --help` | Display help message. |
| `--include-tags=<tags>` | List of tags that will remove the Flows that don't have the provided tags. |
| `--ios-version=<version>` | iOS version. Deprecated: use `--device-os` instead. |
| `--mapping=<path>` | dSYM file for iOS or Proguard mapping file for Android. |
| `--name=<name>` | Name of the upload. |
| `--[no-]ansi, --[no-]color` | Enable / disable colors and ansi output. |
| `--[no-]ansi, --[no-]color` | Enable or turn off colors and ANSI output. ANSI stands for American National Standards Institute. |
| `--device-locale=<locale>` | Set the device locale, for example: "de_DE" for Germany. Use ISO-639-1 and ISO-3166-1 codes. ISO means International Organization for Standardization. |
| `chat` | Use Maestro GPT, the Generative Pre-trained Transformer, to help you with the apps and tests. |
| `mcp` | Start the Maestro Model Context Protocol, also known as MCP. |
| `--headless` | Run the tests in headless mode for web only. |
| `--output=<path>` | File to write report into (default is report.xml). |
| `--projectId, --project-id=<id>` | Project ID. |
| `--pullRequestId, --pull-request-id=<id>` | The ID of the pull request this upload originated from. |
| `--repoName, --repo-name=<name>` | Repository name (for example, GitHub repo slug). |
| `--repoOwner, --repo-owner=<owner>` | Repository owner (for example, GitHub organization or user slug). |
| `--test-suite-name=<name>` | Test suite name. |

### `record`

| Option | Description |
| :--- | :--- |
| `<flowFile>` | The Flow file to record. |
| `[<outputFile>]` | Output file for the rendered video. Only valid for local rendering using `--local`. |
| `[<outputFile>]` | Save the rendered video to this output file. Only works with local rendering using `--local`. |
| `--apple-team-id=<appleTeamId>` | The unique 10-character Apple Team ID assigned to your team's account. |
| `--config=<configFile>` | Optional .yaml configuration file. Defaults to `config.yaml` in the root directory. |
| `--debug-output=<debugOutput>` | Configures a custom path for debug output. |
| `-e, --env=<String=String>` | Environment variables to inject into the Flow. |
| `-h, --help` | Display the help message. |
| `--local` | Beta: Record using local rendering. This becomes the default in a future release. |
| `--local` | Record using local rendering. This is a beta feature and will become the default in a future release. |
| `--output=<path>` | Write the report to this file. The default is report.xml. |
| `--repoName, --repo-name=<name>` | Set the repository name, for example: GitHub repo slug. |
| `--repoOwner, --repo-owner=<owner>` | Set the repository owner, for example: GitHub organization or user slug. |
| `--[no-]ansi, --[no-]color` | Enable or turn off colors and ANSI (American National Standards Institute) output in the terminal. |

### `start-device`

| Option | Description |
| :--- | :--- |
| `--device-locale=<locale>` | Combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code (for example, "de_DE" for Germany). |
| `--device-locale=<locale>` | Use a combination of lowercase ISO-639-1 code and uppercase ISO-3166-1 code, for example: "de_DE" for Germany. |
| `--force-create` | Overrides the existing device if it already exists. |
| `-h, --help` | Display the help message. |
| `--os-version=<version>` | OS version to use. iOS: 16, 17, 18. Android: 28, 29, 30, 31, 33. |
| `--platform=<platform>` | Platforms: `android` or `ios`. |

{% hint style="warning"%}
Some options will be required to run yout tests, like th `<FlowFile>` and the `--parameter` options.
{% endhintß %}