# How Maestro works

Maestro operates as a black-box testing framework that simulates user interactions at the device level. Unlike traditional tools that require access to an app's source code or internal APIs, Maestro leverages the operating system's built-in accessibility and input interfaces to treat the application as an opaque system.

### The "arm's length" philosophy

The central mechanic of Maestro is its "arm's length" operation, meaning the framework pilots the device itself rather than the internal app code.

* **Platform Agnostic**: Because Maestro interacts with the Accessibility Tree (the data layer used by screen readers), it provides a consistent experience across heterogeneous stacks like Native iOS/Android, React Native, and Flutter.
* **Human Simulation**: Maestro reproduces physical actions, like "thumbs on a screen", by sending low-level device commands for tap events, swipe gestures, and text input.
* **System-Wide Control**: Since it controls the device, Maestro can interact with elements outside the app, such as system settings, permission dialogs, and notifications.

### Declarative test definition (YAML)

Tests are defined in simple YAML files, allowing user journeys, referred to as Flows, to be readable as English instructions.

* **Built-in Intelligence**: Maestro features "idiomatic" commands designed to solve common automation hurdles. For example, `scrollUntilVisible` mimics human visual search by automatically scrolling until it finds an element, rather than requiring brittle coordinate-based logic.
* **Built-in Tolerance**: Maestro "embraces instability" by automatically waiting for the screen to "settle" or for content to load, removing the need for manual `sleep()` or artificial wait commands.

{% embed url="https://vimeo.com/744398229?fl=pl&fe=cm" %}

### Maestro ecosystem and workflow

The Maestro suite provides different interfaces to interact with the same core execution engine.

#### Maestro Studio (Visual IDE)

Maestro Studio is the recommended entry point for new users to build tests visually:

1. **Connection**: Studio connects to a device and mirrors the screen to your browser.
2. **Visual Interaction**: You click on elements of the mirrored screen, and Studio identifies them and suggests commands.
3. **Real-time Execution**: Commands are inserted into your YAML file and executed on the device instantly, allowing for step-by-step flow construction.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### Maestro CLI&#x20;

The CLI is the open-source engine that interprets YAML files and sends instructions to the device. It is the primary tool for automated execution in Continuous Integration (CI) systems.

#### Maestro Cloud&#x20;

Maestro Cloud acts as the execution backend for large-scale testing. Teams upload their apps and Flows to run in parallel across multiple hosted virtual devices, ensuring deterministic results and faster feedback loops.

### Advanced logic and modularity

To handle complex scenarios without code duplication, Maestro utilizes modular logic and scripting:

* **Subflows**: Common sequences, such as a "Login" process, can be saved in separate files and called by multiple main tests to facilitate maintenance.
* **Hooks**: Commands like `onFlowStart` and `onFlowComplete` manage app state, such as clearing cache before a test or logging out after completion.
* **JavaScript**: For dynamic data needs (e.g., generating random emails), you can inject small JavaScript snippets that run in a restricted environment without access to the local file system.

### Next steps

To continue your journey with Maestro, choose one of the following options::

* Check the [Broken link](/broken/pages/NYRmrlMy9gNoZWjKSSqO "mention") guide to learn how to install Maestro Studio and run your first test.
* Explore each of the available [our-products](our-products/ "mention").
