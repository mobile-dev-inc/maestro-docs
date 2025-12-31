# How Maestro works

Maestro operates as a black-box testing framework that simulates user interactions at the device level rather than through app APIs or source code instrumentation. This architecture-agnostic approach enables consistent automation across heterogeneous app stacks (native iOS, Android, React Native, Flutter, etc.) by leveraging the device's input/output interfaces.

{% hint style="success" %}
Instead of introspecting app internals, Maestro sends low-level device commands (tap events, swipe gestures, text input via the input method framework) and validates behavior through accessibility APIs and visual element detection, mimicking physical user interaction.
{% endhint %}

Maestro differentiates itself through:
- **Accessibility-First Element Location**: Leveraging platform accessibility for deterministic element identification without brittle coordinate-based selectors.
- **Declarative Test Definition (YAML)**: Human-readable test specifications that abstract platform-specific implementation details.
- **Distributed Cloud Execution**: Parallel test orchestration across multiple emulator/device instances with centralized result aggregation.

### "Arm's length" operation
The central mechanic of Maestro uses "arm's length" operation. This means the framework doesn't interact with the app's source code (such as React Native or Flutter), but rather with the device itself.

*   **Human Simulation**: Maestro works by reproducing the physical actions of a user, like "thumbs on a screen." It sends commands to the device to tap, swipe, or type, ignoring what technology you used to build the app internally.
*   **Device Control**: Because it pilots the device and not just the app, Maestro can interact with elements outside the app, such as system settings menus, permissions, and notifications.

### Test structure (YAML)
Tests aren't written in complex programming languages, but in YAML files. The logic is that the test be readable as a simple English instruction.

*   **Flows**: A test file represents a user scenario (for example, "Book a car").
*   **Declarative Commands**: The user defines direct actions like `tapOn`, `inputText`, or `assertVisible`.
*   **Built-in Intelligence**: Maestro has "idiomatic" commands that solve common automation problems. An example cited is `scrollUntilVisible`: instead of calculating exact coordinates, Maestro automatically scrolls the screen until it finds the desired element, mimicking human visual search behavior.

### Workflow
Practical operation occurs through two main interfaces that interact with the same execution engine:

**A. Via Maestro Studio**
To create and run tests visually:
1.  **Connection**: Studio connects to an emulator or physical device and mirrors the screen to the computer.
2.  **Visual Interaction**: The user clicks on elements of the mirrored screen. Studio identifies the element and suggests commands (for example, tap, validate text).
3.  **Real-time Execution**: When selecting a command, Maestro inserts it into the YAML file and simultaneously executes the action on the device. This allows building and testing the flow step by step instantly.

**B. Via Maestro command-line tool**
For automated execution:
*   The Maestro command-line tool is the engine that interprets YAML files and sends instructions to the connected device. It's frequently used in Continuous Integration (CI) systems to run tests automatically whenever the app code changes.

### Logic and reusability
To function in complex scenarios without duplicating code, Maestro uses:
*   Subflows: Maestro allows extracting code snippets (like a login process) and saving them in separate files. A main test can then execute this "subflow," facilitating maintenance.
*   JavaScript Sandbox: Although the focus is YAML, Maestro allows injecting small JavaScript snippets in a restricted environment (sandbox) to generate random data (like fake emails) or control variables during the test.

### Maestro cloud execution
To scale operation, Maestro cloud acts as an execution backend. The user uploads the app and test files, and the cloud executes these flows in parallel on multiple hosted virtual devices, returning results much faster than local sequential execution.