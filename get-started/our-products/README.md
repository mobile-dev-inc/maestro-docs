# Our solutioions

The Maestro ecosystem comprises three interconnected layers:

* **Maestro Studio** is the interactive IDE layer. It provides real-time device mirroring, element inspection via accessibility APIs, and generates YAML configurations through visual interactions. It abstracts CLI complexity for rapid test development and validation.
* **Maestro CLI** is the core execution engine. It parses YAML test specifications, manages device connectivity (USB/network), handles test orchestration, and outputs structured results. It operates as a headless service suitable for CI/CD pipelines.
* **Maestro Cloud** is the distributed execution platform. It provides infrastructure scaling, parallel test execution across multiple virtual devices, result aggregation, and reporting. It communicates with the CLI via REST APIs to manage remote test runs.

### Maestro CLI (Command Line Interface)
The CLI is the foundational "engine" of the framework. It is open-source and represents the core of Maestro, utilized by over 90% of the user base,.

*   **How it works:** The CLI interprets your test files (written in YAML) and executes the commands directly on a connected device (emulator or physical phone).
*   **Primary Use Case:** It is the tool of choice for technical users who prefer the terminal and is essential for running tests automatically in **CI (Continuous Integration)** systems whenever app code is changed,.
*   **Capabilities:** It offers the most flexibility, supporting specific command-line switches and advanced configurations that may not yet be available in the visual interface.

### Maestro Studio
Maestro Studio is a **GUI (Graphical User Interface)** designed to lower the barrier to entry for new users. It acts as a visual wrapper around the CLI,.

*   **How it works:** When launched, Studio mirrors the connected device's screen on your desktop. It allows you to visually "pick" elements (like buttons or text fields) by clicking on them, which automatically generates the corresponding YAML commands,.
*   **Interactive Workflow:** Unlike traditional coding where you write a script and then run it, Studio functions like an IDE (Integrated Development Environment). It allows you to execute commands on the device and insert them into your test file simultaneously, enabling you to build and validate the test flow step-by-step in real time,.

### Maestro Cloud
Maestro Cloud is the commercial, hosted execution service. While the CLI and Studio are for creating and running tests locally, the Cloud is designed for **scale** and acts as the revenue driver for the company,.

*   **How it works:** It serves as a backend execution environment. You upload your application binary (APK/IPA) and your test files (created via CLI or Studio) to the Cloud. The service then provisions virtual devices to run these tests.
*   **The "Parallelization" Advantage:** The primary benefit of the Cloud is speed. Instead of running 20 tests one after another on a single local machine (which takes a long time), Maestro Cloud can spin up multiple runners to execute all 20 tests simultaneously (in parallel). This provides immediate feedback to the development team.
*   **Integration:** It is not a standalone tool but a destination; you access it via the CLI or Studio to offload the heavy lifting of test execution,.