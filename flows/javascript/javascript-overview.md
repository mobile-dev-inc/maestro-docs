---
description: Extend Maestro flows with JavaScript for complex logic and data manipulation.
---

# JavaScript overview

While Maestro’s YAML syntax is designed to handle the majority of UI interactions declaratively, certain testing scenarios require complex logic that goes beyond simple linear steps. The JavaScript integration allows you to make use of a full-scale scripting engine directly from your Flows, enabling you to handle dynamic data, complex assertions, and external integrations.

### Why use JavaScript in your Flows?

JavaScript provides the flexibility needed to create resilient, data-driven tests without sacrificing the stability. By using JavaScript, you can:

* **Handle Dynamic Data**: Generate unique identifiers, format dates, or manipulate strings for input fields.
* **Complex Control Flow**: Implement logic that YAML cannot express easily, such as complex mathematical calculations or multi-step conditional branching.
* **External Connectivity**: Sync your UI tests with your backend by making API calls to fetch test data or verify database states.
* **Enhanced Assertions**: Write custom logic to verify UI states that require calculation or data parsing.

### How it works

To ensure that tests remain portable and secure, Maestro executes JavaScript in a restricted sandbox. This means the scripts run in a "clean" environment without direct access to your local file system or external Node.js libraries. This architecture ensures that a Flow written on one machine will behave identically on a teammate's computer or in Maestro Cloud.

{% hint style="info" %}
#### JavaScript engine support

In Maestro, the GraalJS engine is enabled by default, allowing you to use modern ECMAScript (ES6+) features.

Rhino is also supported, but it must be explicitly enabled. Maestro discourage the Rhino usage.
{% endhint %}

### Explore JavaScript capabilities

Navigate through these guides to master scripting within your automation suite:

* [run-and-debug-javascript.md](run-and-debug-javascript.md "mention"): Maestro provides three ways to run JavaScrip. You can also use standard `console.log` statements to debug your logic during execution.
* [manage-data-and-states.md](manage-data-and-states.md "mention"): The global `output` object allows you to share data across your entire Flow. This ensures that a value captured or generated in one script can be used by any subsequent YAML command or JavaScript expression.
* [make-http-requests.md](make-http-requests.md "mention"): With the built-in HTTP client, you can perform `GET`, `POST`, `PUT`, and `DELETE` requests directly from your scripts.&#x20;
* [generate-synthetic-data.md](generate-synthetic-data.md "mention"): The `faker` object integration enables the generation of randomized data to ensure every test run uses fresh data and avoids account collisions.
