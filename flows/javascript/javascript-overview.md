# JavaScript overview

While Maestro’s YAML syntax is designed to handle the majority of UI interactions declaratively, certain testing scenarios require complex logic that goes beyond simple linear steps. The JavaScript integration allows you to embed a full-scale scripting engine directly into your Flows, enabling you to handle dynamic data, complex assertions, and external integrations.

### Why use JavaScript in your Flows?

The goal of the JavaScript feature is to provide flexibility without sacrificing stability. By using JS, you can:

* **Handle Dynamic Data**: Generate unique identifiers, format dates, or manipulate strings for input fields.
* **Complex Control Flow**: Implement logic that YAML cannot express easily, such as complex mathematical calculations or multi-step conditional branching.
* **External Connectivity**: Sync your UI tests with your backend by making API calls to fetch test data or verify database states.
* **Enhanced Assertions**: Write custom logic to verify UI states that require calculation or data parsing.

### How it Works

To ensure that tests remain portable and secure, Maestro executes JavaScript in a restricted sandbox. This means the scripts run in a "clean" environment without direct access to your local file system or external Node.js libraries. This architecture ensures that a Flow written on one machine will behave identically in Maestro Cloud or on a teammate's computer.

### Explore JavaScript capabilities

Navigate through these guides to master scripting within your automation suite:

* [javascript-on-maestro-flows.md](javascript-on-maestro-flows.md "mention"): Learn the different ways to inject JS: using inline expressions `${...}` or executing external `.js` files via the `runScript` command.
* [javascript-outputs.md](javascript-outputs.md "mention"): Understand how to store values from your scripts into a global `output` object so they can be reused by subsequent YAML commands.
* [maestro-support-for-graaljs.md](maestro-support-for-graaljs.md "mention"): Learn how to enable the GraalJS engine to use modern ECMAScript features (ES6+) for cleaner and more powerful script logic.
* [how-to-use-logging.md](how-to-use-logging.md "mention"): Master the use of `console.log()` to output data to the Maestro console, helping you debug complex scripts and variable states during execution.
* [how-to-generate-random-data.md](how-to-generate-random-data.md "mention"): Explore the guide on creating unique emails, names, or numbers to ensure every test run uses fresh data and avoids account collisions.
* [how-to-make-http-requests.md](how-to-make-http-requests.md "mention"):  Learn how to use the built-in `http` module to communicate with your APIs for data seeding or state verification.
* [how-to-access-text-elements.md](how-to-access-text-elements.md "mention"): Discover how to programmatically read and manipulate text content from the screen for advanced validation logic.
