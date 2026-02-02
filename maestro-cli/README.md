# Maestro CLI overview

The Maestro CLI is an open-source, single-binary framework designed for end-to-end mobile and web UI testing. It allows developers and testers to define user journeys, referred to as [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/), using a declarative YAML syntax that is easy to read and maintain.

### Learn how to use Maestro CLI

To master the Maestro CLI, we suggest you explore the following path:

1. [How to Install Maestro CLI](how-to-install-maestro-cli/): Step-by-step instructions for macOS, Linux, and Windows.
2. [Run your first test using the Maestro CLI](run-your-first-test-with-the-maestro-cli.md): Learn how to execute your first test using the CLI.
3. [Reference for Maestro CLI](https://www.google.com/search?q=https://docs.maestro.dev/maestro-cli/reference): Explore all CLI commands available and their arguments.
4. [How to Setup Maestro with WSL2](how-to-setup-maestro-with-wsl2.md): Check how to run Maestro in a Windows Subsystem for Linux environment.
5. [Install Android on WSL2](https://www.google.com/search?q=https://docs.maestro.dev/maestro-cli/android-wsl2): Specific configuration for Android emulators in WSL2.
6. [Troubleshooting](https://www.google.com/search?q=https://docs.maestro.dev/maestro-cli/troubleshooting): Verify common issues and solutions for local and environment setups.

### Maestro CLI features

The CLI serves as the central engine for multiple automation workflows. Whether you prefer using Maestro Studio or your own IDE, the CLI handles the execution against emulators, simulators or physical devices. With Maestro CLI you can:

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Run Local Tests</strong></td><td>Execute tests against a running emulator/simulator or physical device using the command <code>maestro test flow.yaml</code>.</td></tr><tr><td><strong>Continuous Development</strong></td><td>The Continuous Mode (<code>maestro test -c</code>) monitors your YAML test files for changes and automatically restarts the test upon saving.</td></tr><tr><td><strong>Scale to the Cloud</strong></td><td>Upload your Flows to Maestro Cloud to run tests at scale across a variety of managed device configurations.</td></tr><tr><td><strong>Manage Devices</strong></td><td>Create and launch Android emulators or iOS simulators that match specific configurations using the <code>maestro start-device</code> command.</td></tr><tr><td><strong>Debug</strong></td><td>Identification of selectors is simplified with commands like <code>maestro hierarchy</code>, which prints the current app’s view hierarchy directly to the terminal.</td></tr></tbody></table>

### Core Features

Maestro is built on the philosophy of "embracing instability," providing a suite of features that move beyond traditional automation tools:

<table data-header-hidden><thead><tr><th width="229.5555419921875"></th><th></th></tr></thead><tbody><tr><td><strong>Feature</strong></td><td><strong>Description</strong></td></tr><tr><td>Built-in Tolerance</td><td>Automatically handles network delays and UI flakiness by waiting for the screen to "settle" before proceeding.</td></tr><tr><td>Extensive Commands</td><td>A library of commands for UI interactions (<code>tapOn</code>, <code>swipe</code>), navigation (<code>launchApp</code>, <code>openLink</code>), and device control.</td></tr><tr><td>JavaScript Integration</td><td>Inject JavaScript directly into YAML or run external scripts (<code>runScript</code>) for complex logic, such as generating random email addresses, or making HTTP requests. </td></tr><tr><td>Modularity</td><td>Create composable subflows that can be reused across multiple tests to keep your automation suite DRY (Don't Repeat Yourself).</td></tr><tr><td>AI-Powered Testing</td><td>Verify complex UI with natural language (<code>assertWithAI</code>) and generate LLM-based analysis reports.</td></tr><tr><td>Flow Recording</td><td>The <code>maestro record</code> command stitches screen recordings and test output into a shareable MP4 video.</td></tr></tbody></table>

### Next Step

Learn how to get started with our [How to Install Maestro CLI](how-to-install-maestro-cli/) guide.
