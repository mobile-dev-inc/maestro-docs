# Maestro Flows overview

Maestro Flows are the fundamental building blocks of UI automation, representing specific segments of a user journey, such as Login, Checkout, or Search for an item, within an application. Flows can represent complete user journeys or discrete functional components that can be composed into larger test scenarios. By modeling real-world user interactions, Flows provide a reliable, repeatable way to verify app behavior across Android, iOS, and Web platforms from a single suite.

#### The anatomy of a Flow

Flows are written in a human-readable YAML format, designed to be understood and maintained by both developers and manual testers without heavy programming knowledge.

A standard Flow consists of two main parts:

* **Configuration Section**: Defined at the top (above the `---` marker), this includes the `appId` of the app under test, along with optional metadata like `name`, `tags`, and environment variables.
* **Workflow Section**: A sequence of declarative commands, such as `tapOn` and `inputText`, that simulate user actions and validate the UI state.

```yaml
# --- Configuration Section ---
appId: com.example.app         # Mandatory: Define the ID of the app under test
name: My Login Flow            # Optional: Customize the Flow name
tags:                          # Optional: Filter which tests to run
  - smoke-test
env:                           # Optional: Map of environment variables
  USERNAME: "user@example.com"

# --- Workflow Section ---
- launchApp                    # Launches the application
- tapOn: "Username"            # Interacts with the username field
- inputText: ${USERNAME}       # Inputs the environment variable
- tapOn: "Login"               # Taps the login button
- assertVisible: "Welcome"     # Verifies success message appears
```

### Explore Flows capabilities

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><i class="fa-gear">:gear:</i></td><td><strong>Flow control and logic</strong></td><td>Build resilient, intelligent journeys. Master the architectural tools used to scale your tests, including modular subflows, conditional branching, repetitive loops, and lifecycle hooks.</td><td><a href="flow-control-and-logic/flow-control-and-logic-overview.md">flow-control-and-logic-overview.md</a></td></tr><tr><td><i class="fa-node-js">:node-js:</i></td><td><strong>JavaScript</strong></td><td>Extend YAML with custom scripting. Use the integrated JavaScript sandbox to handle complex data, generate random test variables, capture script outputs, and interact with external APIs via HTTP requests.</td><td><a href="javascript/javascript-overview.md">javascript-overview.md</a></td></tr></tbody></table>



### Next step

Learn the best practices for organizing your Flows into a scalable [Test Suite](how-to-structure-your-test-suite.md) that can handle enterprise-level app complexity.
