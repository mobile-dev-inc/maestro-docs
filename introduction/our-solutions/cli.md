# Maestro CLI

The **Maestro command-line tool** is the fundamental foundation and open source "engine" of the entire Maestro ecosystem. While Maestro Studio provides a visual interface, it's the command-line tool that interprets YAML files and effectively executes commands on devices.

Currently, approximately **90% of Maestro's user base** uses the command-line tool, making it the standard tool for running local tests and integrating with development pipelines.

## Key functions and responsibilities

The Maestro command-line tool serves three primary roles in the test automation workflow: as the core execution engine that interprets YAML files and controls devices, as the automation backbone for continuous integration pipelines, and as a power tool offering advanced features beyond the graphical interface. Understanding these distinct capabilities helps teams leverage the command-line tool effectively across different stages of development and testing.

### The execution engine
The command-line tool is the component responsible for reading test files (`.yaml`), connecting to the device (physical or emulator), and translating instructions into real actions, such as taps and swipes.
*   **Independence:** It runs directly in your machine's terminal and doesn't require a graphical interface to function, making it extremely lightweight and fast.
*   **Compatibility:** Works for both running local tests and as a gateway to send tests for execution in Maestro Cloud.

### Automation and CI/CD (continuous integration)
The most critical use case for the command-line tool is automation. While Maestro Studio is ideal for *creating* tests, the command-line tool is the standard tool for *running* those tests recurrently and autonomously.
*   **Pipelines:** Developers configure the command-line tool in CI systems (such as GitHub Actions or Jenkins) so that tests run automatically whenever the app code changes.
*   **Hybrid Workflow:** It's common for teams to use Studio to build tests visually and then use the command-line tool to execute that same YAML file in their continuous validation processes.

### Flexibility and advanced features
The command-line tool offers a level of granular control that sometimes exceeds the capabilities of Studio's visual interface.
*   **Command Options:** There are "switches" (command-line parameters) and advanced configurations available in the command-line tool that Studio's graphical interface hasn't yet implemented.
*   **Utility Commands:** The command-line tool includes helper tools, such as the `download-samples` command, which downloads project examples (like Wikipedia) for quick learning, and specific commands for managing *workspace* configurations.

## Command-line tool vs. Studio

It's important to understand that Studio acts as a *wrapper* (a layer) over the command-line tool. Studio depends on the command-line tool to function.

| Feature | Maestro command-line tool | Maestro Studio |
| :--- | :--- | :--- |
| **Focus** | Execution, Automation, and CI/CD | Test Creation and Maintenance |
| **Interface** | Terminal (Command Line) | GUI (Graphical Interface in Browser) |
| **Workflow** | Text Editor + Terminal | Interactive (Point-and-click) |
| **Audience** | DevOps Engineers, Developers | Manual QAs, Beginners, Test Creators |