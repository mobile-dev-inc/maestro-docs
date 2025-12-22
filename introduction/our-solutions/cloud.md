# Maestro cloud and continuous integration (CI)

While the **Maestro command-line tool** and **Maestro Studio** are tools focused on creating and validating tests locally, **Maestro cloud** is the infrastructure solution designed for **scale, speed, and automation**.

This page details how Maestro cloud functions as an execution backend and how it integrates with your CI/CD pipelines to ensure app quality with every new code change.

## What's Maestro cloud?
Maestro cloud is a hosted execution service that allows you to run your test flows (`.yaml`) on virtual devices managed in the cloud, eliminating the need to set up and maintain your own device or emulator farm.

It acts as the final destination for mass test execution. You upload your app (APK or IPA) and test files, and the cloud handles infrastructure provisioning and execution.

### The power of parallelization
The main technical and business advantage of Maestro cloud is **parallelization**.
*   **Local Execution (Serial):** When running tests locally via the command-line tool, they execute one after another (sequentially). If you have 20 tests and each takes 2 minutes, feedback takes 40 minutes.
*   **Cloud Execution (Parallel):** Maestro cloud can allocate multiple runners simultaneously. If you upload the same 20 tests, the cloud can start 10 or more devices at once, drastically reducing total feedback time.

## Continuous integration (CI)
Automation via CI is the most critical use case for ensuring that "the ride booking flow" or "login" continues working whenever a developer changes code.

### How the CI flow works
While **Maestro Studio** is often used to *create* tests visually, it's the **Maestro command-line tool** that typically orchestrates automatic execution within CI systems (such as GitHub Actions, Jenkins, CircleCI).

1.  **Trigger:** A developer pushes a code change (Push/Pull Request).
2.  **Build:** The CI system compiles the new app binary.
3.  **Command:** The CI script uses the command-line tool command (for example, `maestro cloud`) to send the new binary and existing test flows to Maestro cloud.
4.  **Execution:** The cloud runs tests in parallel.
5.  **Result:** The CI system receives the status (Passed/Failed), blocking or approving the change.

### Studio as gateway
It's important to note that Maestro cloud isn't an isolated product requiring separate installation. It integrates into the tools you already use. Maestro Studio acts as a "gateway" or entry point, facilitating upload and initial cloud execution without requiring complex terminal commands during the exploration phase.

## Differentiation: local vs. cloud

| Feature | Local Execution (command-line tool/Studio) | Maestro cloud |
| :--- | :--- | :--- |
| **Infrastructure** | Your Computer / Local Emulator | Managed cloud Devices |
| **Speed** | Sequential (One at a time) | Parallel (Multiple simultaneous) |
| **Focus** | Creation, Debug, and Unit Tests | Complete Regression and CI/CD |
| **Cost** | Free (Open Source) | Commercial Service (Revenue Driver) |

{% hint style="success" %}
Maestro's vision is that test creation should be accessible and simple (via Studio), but quality validation at scale occurs in the cloud, ensuring development teams have absolute confidence in end-user experience before each release.
{% endhint %}