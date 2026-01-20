---
hidden: true
---

# Core concepts

Traditional testing tools operate like unit testers inspecting internal APIs—they require instrumentation, framework knowledge, and access to the app's source code to validate individual components. Maestro operates like an end-to-end black-box testing framework—it interacts with the UI layer through the accessibility tree and input events, treating the app as an opaque system. This approach eliminates framework dependencies, reduces test maintenance overhead, and validates the complete user experience stack without requiring knowledge of implementation details or internal state management.

## What's maestro?

Maestro is a mobile app test automation framework (Android and iOS) focused on simplicity and reliability. Unlike traditional tools that require deep integration with source code, Maestro operates by simulating real user interactions.

The core value proposition is eliminating three main problems with traditional testing tools: complexity, flakiness, and high technical barriers to entry.

## "Arm's length" philosophy

One of Maestro's most important concepts is its "arm's length" approach.

* Code Independence: Maestro doesn't need to know what technology you used to build the app (whether it's React Native, Flutter, or Native). It "pilots" the device, not the app code.
* Human Simulation: The framework reproduces the behavior of "human thumbs on a screen." This means it interacts with the UI visually, allowing you to test not just the app but interactions with the operating system (like changing device settings).
* Black Box: Because it doesn't access internal code, tests ensure that the end-user experience is working, rather than just testing if a specific code function responds correctly.

## The maestro product suite

Maestro's ecosystem consists of three interconnected parts, each serving a specific purpose in the workflow:

### Maestro command-line tool

* The Engine: It's the open source foundation of the tool. It executes test files (YAML) locally on emulators or physical devices.
* Usage: Ideal for continuous integration (CI) and technical users who prefer the terminal. About 90% of the user base uses the command-line tool.

### Maestro Studio (GUI)

* Visual Interface: A graphical tool that acts as a wrapper for the command-line tool. It allows you to create tests visually by clicking on elements on the connected device's screen.
* Entry Point: Positioned as the recommended entry point for new users, as it eases the learning curve and element inspection.
* Interactivity: Allows you to build and execute commands line by line in real time, functioning almost like an IDE for testing.

### Maestro cloud

* Scale Execution: A hosted service that allows you to run tests in the cloud. The main benefit is parallelization, allowing you to run multiple test flows simultaneously for quick feedback.
* Business Model: It's the company's primary revenue driver, serving as the execution backend for tests created via the command-line tool or Studio.

## Technical concepts and syntax

### YAML syntax

You write Maestro tests in YAML files, a simple and readable language. This removes the need for deep programming knowledge (like JavaScript or Java) to write tests, making the tool accessible to manual and non-technical QAs.

### Test structure

* Flows: The test script. A YAML file that describes a user journey (for example, "Login," "Book a car").
* Subflows: Maestro encourages code reuse. You can save common snippets, like "logging in," as subflows and reuse them across multiple different tests, avoiding repetition.
* Hooks: Commands like `onFlowStart` or `onFlowComplete` allow you to configure the app state before testing (for example, clear cache, launch the app) or perform actions when finished.

### Main commands

Interaction uses intuitive commands that mimic physical actions:

* Tap / Input Text: Tap elements and type text.
* Scroll Until Visible: An "idiomatic" and convenient command that automatically scrolls the screen until it finds the desired element, simulating a user's visual search.
* Assert: Checks if an element is visible on the screen to validate the success of an action.

### JavaScript (sandbox)

For more advanced logic, Maestro allows you to inject small JavaScript snippets (for example, generate a random email or create loops), but it runs in a restricted environment (sandbox) without access to external libraries or the file system.

## Target audience and adoption

* Accessibility: Designed so that anyone on the team, from developers to manual QAs with no coding experience, can create automation.
* Market Credibility: Used by large companies like Microsoft, Doordash, and Kraken, which reinforces its position as a reliable tool for complex scenarios.
