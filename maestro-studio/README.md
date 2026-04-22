---
description: >-
  Maestro Studio is the desktop app for writing, running, and debugging mobile
  UI tests visually, using simple YAML files and a live connection to your
  device.
---

# Maestro Studio overview

With Maestro Studio you can connect a device, build your tests by interacting directly with your app, and run them without switching tools.

### Learn how to use Maestro Studio

To start using Maestro Studio, Explore the following path:

1. Visit [run-tests-with-maestro-studio.md](run-tests-with-maestro-studio.md "mention") to install the Studio and create and run your first test.
2. Explore [environments-and-variables.md](environments-and-variables.md "mention") to learn how to handle dynamic data and secrets directly within the visual editor.
3. Use the [run-cloud-tests-from-maestro-studio.md](run-cloud-tests-from-maestro-studio.md "mention") to run your tests on Maestro Cloud directly from Studio.

### What you can do in Studio

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Write tests faster</strong></td><td>Type a hyphen in the YAML editor to see all available Maestro commands. Autocomplete suggests commands, arguments, and real selectors pulled from your connected device's screen, so you spend less time in the docs and fewer errors make it to run time.</td></tr><tr><td><strong>Visual test creation</strong></td><td>Right-click any element on your connected device to add YAML commands directly to your test. No need to manually look up element IDs or selectors. </td></tr><tr><td><strong>Run and debug locally</strong></td><td>Run your tests step by step and see exactly what happens on screen at each stage. Every run is recorded, so you can jump to any point and inspect what went wrong.</td></tr></tbody></table>

### Maestro Studio vs. Maestro CLI

Maestro is also available via [CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/). However, while the Maestro CLI is the core engine for executing tests and CI/CD integration, the Maestro Studio  is a specialized layer designed for development and debugging.

| **Feature**       | **Maestro Studio**                                                | **Maestro CLI**                               |
| ----------------- | ----------------------------------------------------------------- | --------------------------------------------- |
| Primary Interface | Visual GUI / Desktop App                                          | Terminal / Command Line                       |
| Core Purpose      | Writing, running, and debugging tests visually.                   | Executing test suites in CI/CD.               |
| Setup Required    | Requires Android SDK and/or Xcode to run against virtual devices. | Requires Java 17+, Android SDK, and Xcode.    |
| Inspection Tool   | Point-and-click interface to see what Maestro sees.               | Uses `maestro hierarchy` for terminal output. |

