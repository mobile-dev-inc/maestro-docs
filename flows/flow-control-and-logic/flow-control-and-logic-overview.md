# Flow control and logic overview

While standard Flows represent linear user journeys, real-world testing often requires dynamic behavior. The documentation from this section covers the tools that allow your tests to adapt to different application states, platform requirements, and data environments.

### Core Pillars of Flow Architecture

To build scalable tests, you will utilize four primary logical patterns:

#### **1. Modularity**

Avoid repeating yourself, you can use [Nested Flows](nested-flows.md) to extract common journeys, like Login or Onboarding, into separate files. You can then call these "subflows" across your entire suite using the `runFlow` command.

#### **2. Conditional execution**

Not every test step should run every time. [Conditions](conditions.md) allow you to execute actions based on element visibility, platform (iOS vs. Android), or custom JavaScript expressions.

#### **3. Repetition**&#x20;

Handle dynamic lists or "polling" scenarios with [Loops ](loops.md)to repeat actions until a goal is met. Complement this with [Wait Commands](wait-commands.md) to ensure your tests only proceed when the UI is stable, eliminating flakiness from slow network loads.

#### **4. Environment and life-cycle**

Manage test data externally using [Parameters ](parameters.md)and [Constants](constants.md), allowing the same Flow to run in Staging, QA, or Production. Use [Hooks ](hooks.md)(`onFlowStart`, `onFlowComplete`) to automate setup and teardown tasks, such as clearing app state or granting [Permissions](permissions.md).

### How to Explore This Section

We recommend exploring these features in the following order:

1. Start with [Nested Flows](nested-flows.md): Learn how to break your tests into manageable parts.
2. Add [Conditions](conditions.md): Make your modular tests smarter by handling "if-then" scenarios.
3. Optimize with [Parameters](parameters.md): Replace hardcoded data with dynamic variables to support multiple environments.
4. Finalize with [Hooks](hooks.md): Ensure every test run starts from a clean, reliable state.

