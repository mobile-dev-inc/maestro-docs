---
description: >-
  Maestro CLI overview: install, configure, and run mobile UI tests from your
  terminal.
---

# Maestro CLI overview

The Maestro CLI is an open-source, single-binary framework designed for end-to-end mobile and web UI testing. It allows developers and testers to define user journeys, referred to as [Flows](https://app.gitbook.com/o/zCVYm3M93B0sOcjR1Oj4/s/mS3lsb9jRwfRHqddeRXG/), using a simple, declarative YAML syntax.

### Learn how to use Maestro CLI

To get up and running with the Maestro CLI, follow these foundational steps:

1. [Installation](how-to-install-maestro-cli/): Step-by-step instructions for installing the Maestro CLI on macOS, Windows, WSL, and Linux.
2. [Run your first test](run-your-first-test-with-the-maestro-cli.md): A hands-on guide to writing and executing your first Flow on an Android emulator.
3. [Maestro CLI reference](maestro-cli-commands-and-options.md): A complete list of all global options and subcommands.

{% hint style="info" %}
If you are using WSL and encounter issues running tests, see the [Troubleshooting](troubleshooting-wsl2-and-android-connections.md) page for additional guidance.
{% endhint %}

### Maestro CLI features

The CLI serves as the central engine for multiple automation workflows. Whether you prefer using Maestro Studio or your own IDE, the CLI handles the execution against emulators, simulators or physical devices. With Maestro CLI you can:

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Run Local Tests</strong></td><td>Execute tests against a running emulator/simulator or physical device using the command <code>maestro test flow.yaml</code>.</td></tr><tr><td><strong>Continuous Development</strong></td><td>The Continuous Mode (<code>maestro test -c</code>) monitors your YAML test files for changes and automatically restarts the test upon saving.</td></tr><tr><td><strong>Device Management</strong></td><td>Create and launch specific emulator or simulator configurations with <code>maestro start-device</code>.</td></tr><tr><td><strong>Scale to the Cloud</strong></td><td>Upload your Flows to Maestro Cloud to run tests at scale across a variety of managed device configurations.</td></tr><tr><td><strong>Debug Tools</strong></td><td>Identification of selectors is simplified with commands like <code>maestro hierarchy</code>, which prints the current app’s view hierarchy directly to the terminal.</td></tr></tbody></table>

### Core Features

Maestro is built on the philosophy of "embracing instability," providing a suite of features that move beyond traditional automation tools:

<table data-header-hidden><thead><tr><th width="229.5555419921875"></th><th></th></tr></thead><tbody><tr><td><strong>Feature</strong></td><td><strong>Description</strong></td></tr><tr><td>Built-in Tolerance</td><td>Automatically handles network delays and UI flakiness by waiting for the screen to "settle" before proceeding.</td></tr><tr><td>Extensive Commands</td><td>A library of commands for UI interactions (<code>tapOn</code>, <code>swipe</code>), navigation (<code>launchApp</code>, <code>openLink</code>), and device control.</td></tr><tr><td>JavaScript Integration</td><td>Run JavaScript expressions directly from YAML to manage complex data or perform HTTP requests</td></tr><tr><td>Modularity</td><td>Create composable subflows that can be reused across multiple tests to keep your automation suite DRY (Don't Repeat Yourself).</td></tr><tr><td>Flow Recording</td><td>The <code>maestro record</code> command stitches screen recordings and test output into a shareable MP4 video.</td></tr><tr><td>AI Analysis</td><td>[Beta] Generate LLM-based analysis reports for UI and internationalization issues.</td></tr></tbody></table>

### Next Step

Learn how to get started with Maestro accessing the [How to install Maestro CLI](how-to-install-maestro-cli/) guide.
