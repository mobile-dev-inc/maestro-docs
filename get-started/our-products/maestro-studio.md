---
hidden: true
---

# Maestro Studio

**Maestro Studio** serves as the interactive graphical user interface (GUI) for the Maestro framework, offering a sophisticated visual development environment tailored for the creation, debugging, and execution of test automation scripts. By abstracting the manual YAML authoring process, it enables declarative test creation through intuitive point-and-click interactions with mirrored device screens.

This tool significantly reduces the technical barrier for test automation by eliminating the necessity for manual inspection of view hierarchies or the tedious task of writing YAML syntax from scratch. It operates as a browser-based interface over the Maestro command-line tool, seamlessly integrating device interaction, real-time command generation, and test execution into a cohesive workflow.

Upon connecting to a device (either an emulator or a physical device), Studio mirrors the display within your browser, allowing direct interaction with UI elements. The framework automatically captures essential element properties (such as accessibility IDs, text content, and hierarchy coordinates) and generates corresponding YAML commands (`tapOn`, `inputText`, `assertVisible`) in real-time, facilitating iterative test development with immediate visual feedback.

## Key features

The primary features of Maestro Studio include:

* **Visual inspection and command generation**: Maestro Studio eliminates the guesswork associated with identifying element IDs within the Android or iOS view hierarchy:
  * **Point and Click:** Clicking on an element in the mirrored screen (for example, a button or text field) prompts Studio to automatically identify and display that element's properties (text, ID, etc.).
  * **Automatic Generation:** Based on your selection, Studio intelligently suggests valid YAML commands (for example, `tapOn`, `inputText`, `assertVisible`) and integrates them into the test file.
* **Interactive execution (REPL)**: Maestro Studio functions similarly to an Integrated Development Environment (IDE), allowing you to construct your test incrementally in real-time:
  * **Execute and Insert:** You can execute isolated commands to verify their capability on the device, and upon success, permanently insert them into the test flow.
  * **Instant Feedback:** This feature enables immediate validation of test logic, circumventing the traditional cycle of "write everything, run, fail, fix, and run again."
* **Intelligent element search**: Leveraging Maestro's "Computer Vision" capabilities, Studio comprehends the screen hierarchy, simplifying the creation of assertions (validations) to ensure specific text or icons are visible post-action.

## Recommended workflow

While Maestro can be fully operated via the command-line tool, Studio enhances the efficiency of new flow creation.

1. **Creation in Studio:** Utilize Maestro Studio to navigate the app, identify elements, and interactively construct the foundational structure of your YAML file (`flow.yaml`).
2. **Refinement and CI:** Once you generate the YAML file, it becomes a standard text file. You can subsequently edit it to incorporate complex logic (such as subflows or JavaScript scripts) and execute it through the **Maestro command-line tool** in your Continuous Integration (CI) pipelines or on **Maestro cloud**.

## Differences: Studio vs. command-line tool

It's crucial to understand that both Studio and the command-line tool utilize the same underlying "engine." Studio serves as a visual interface that enhances interaction, while the final output (the YAML file and device execution) remains consistent.

| Feature            | Maestro Studio                | Maestro command-line tool           |
| ------------------ | ----------------------------- | ----------------------------------- |
| **Interface**      | Visual (GUI) in Browser       | Terminal / Command Line             |
| **Primary Use**    | Test creation and exploration | Mass execution and CI/CD            |
| **Learning Curve** | Low (Ideal for beginners)     | Medium (Requires command knowledge) |
| **Interactivity**  | High (Point and click)        | Low (Ready-made script execution)   |

{% hint style="info" %}
Although Studio is the preferred tool for creation, certain advanced configuration features and specific execution switches may only be accessible via the command-line tool.
{% endhint %}
