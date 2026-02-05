---
description: >-
  Visual development environment to build tests by clicking on elements,
  auto-generating YAML, and running commands interactively on your device.
---

# Maestro Studio overview

Maestro Studio is a visual development environment designed to accelerate the creation of test flows by allowing users to interact with their applications graphically. Instead of writing YAML from scratch, users can build robust tests by simply clicking on elements within their app, effectively bridging the gap between manual interaction and automated scripting.

### Learn how to use Maestro Studio

To start using the Maestro Studio, we suggest you to explore the following path:

1. Visit [How to install Maestro Studio](/broken/spaces/CbCMt5C3rawmE9oIus7f/pages/Gkh2PaXSFN0gAJQLxuIc) and [How to run your first test](/broken/spaces/CbCMt5C3rawmE9oIus7f/pages/kmqn1gss5nFaFJkY1CCh) to set up your environment in under a minute.
2. Explore [Environment variables](environment-variables.md) to learn how to handle dynamic data and secrets directly within the visual editor.
3. Use the [Run Cloud tests from Maestro Studio](run-cloud-tests-from-maestro-studio.md) guide to learn how to trigger enterprise-grade cloud runs with a single click.

### Maestro Studio capabilities

Maestro Studio acts as an interactive playground for authoring mobile and web tests.

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Visual Element Selection</strong></td><td>Select UI elements like icons or buttons using the live app. Studio identifies the exact accessibility ID or text needed, eliminating the need to guess selectors.</td></tr><tr><td><strong>Automatic YAML Generation</strong></td><td>Upon selecting an element, Studio automatically generates YAML command examples (such as <code>tapOn</code> or <code>assertVisible</code>) that can be executed directly, added to your test file, or both.</td></tr><tr><td><strong>Interactive Action Runner</strong></td><td>Execute individual Maestro commands on the fly to see their effects on your device immediately, without needing to restart your entire test suite.</td></tr></tbody></table>

### Maestro Studio vs. Maestro CLI

Maestro is also available via [CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/). However, while the Maestro CLI is the core engine for executing tests and CI/CD integration, the Maestro Studio  is a specialized layer designed for development and debugging.

| **Feature**       | **Maestro Studio**                                                                     | **Maestro CLI**                               |
| ----------------- | -------------------------------------------------------------------------------------- | --------------------------------------------- |
| Primary Interface | Visual GUI / Desktop App                                                               | Terminal / Command Line                       |
| Core Purpose      | authoring, debugging, and visual inspection.                                           | Executing test suites in CI/CD.               |
| Setup Required    | Studio Desktop requires zero CLI or IDE setup. But it requires Android SDK, and Xcode. | Requires Java 17+, Android SDK, and Xcode.    |
| Inspection Tool   | Point-and-click interface to see what Maestro sees.                                    | Uses `maestro hierarchy` for terminal output. |

### Next step

Are you completely new to Maestro? Start with our [QuickStart](https://app.gitbook.com/s/CbCMt5C3rawmE9oIus7f/get-started/quickstart "mention") for a high-level overview.

If you decided to use Maestro Studio, get started by learning [how-to-install-maestro-studio.md](how-to-install-maestro-studio.md "mention").
