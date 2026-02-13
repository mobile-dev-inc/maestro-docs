---
description: >-
  Maestro Studio is a visual development environment to build tests  based on
  YAML files by interacting with your application.
---

# Maestro Studio overview

Maestro Studio is a visual development environment designed to accelerate the creation of test flows by allowing users to interact with their applications graphically. Instead of writing from scratch, users can build robust tests in YAML files by visually interacting with their app, accelerating the transition from manual testing to automated scripting.

### Learn how to use Maestro Studio

To start using Maestro Studio, Explore the following path:

1. Visit [run-tests-with-maestro-studio.md](run-tests-with-maestro-studio.md "mention") to install the IDE and create and run your first test.
2. Explore [environments-and-variables.md](environments-and-variables.md "mention") to learn how to handle dynamic data and secrets directly within the visual editor.
3. Use the [run-cloud-tests-from-maestro-studio.md](run-cloud-tests-from-maestro-studio.md "mention") guide to learn how to trigger enterprise-grade cloud runs with a single click.

### Maestro Studio capabilities

Maestro Studio acts as an interactive playground for authoring mobile and web tests.

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Visual Element Selection</strong></td><td>Select UI elements like icons or buttons using the live app. Studio identifies the exact accessibility ID or text needed, eliminating the need to guess selectors.</td></tr><tr><td><strong>Automatic YAML Generation</strong></td><td>Upon selecting an element, Studio automatically generates YAML command examples (such as <code>tapOn</code> or <code>assertVisible</code>) that can be executed directly, added to your test file, or both.</td></tr><tr><td><strong>Interactive Action Runner</strong></td><td>Execute individual Maestro commands on the fly to see their effects on your device immediately. This  allows you to build your test step-by-step in the preview window.</td></tr></tbody></table>

### Maestro Studio vs. Maestro CLI

Maestro is also available via [CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/). However, while the Maestro CLI is the core engine for executing tests and CI/CD integration, the Maestro Studio  is a specialized layer designed for development and debugging.

| **Feature**       | **Maestro Studio**                                                | **Maestro CLI**                               |
| ----------------- | ----------------------------------------------------------------- | --------------------------------------------- |
| Primary Interface | Visual GUI / Desktop App                                          | Terminal / Command Line                       |
| Core Purpose      | Aauthoring, debugging, and visual inspection.                     | Executing test suites in CI/CD.               |
| Setup Required    | Requires Android SDK and/or Xcode to run against virtual devices. | Requires Java 17+, Android SDK, and Xcode.    |
| Inspection Tool   | Point-and-click interface to see what Maestro sees.               | Uses `maestro hierarchy` for terminal output. |

