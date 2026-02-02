# Maestro Cloud overview

Maestro Cloud is a hosted, enterprise-grade infrastructure designed to execute automated tests with high parallelism and reliable scaling. It allows teams to run their "Flows" in a stable, managed environment, eliminating the need to configure or maintain local emulators and simulators.

By offloading device management to the cloud, teams can reduce test execution time by up to 90% through asynchronous parallel runs, enabling faster shipping cycles with increased confidence.

### Learn how to use Maestro Cloud

Follow these guides to set up your cloud testing environment:

1. [How to run your tests on Maestro Cloud](how-to-run-your-tests-on-maestro-cloud.md): A step-by-step tutorial on prerequisites and your first cloud upload.
2. [CI Integration](ci-cd-integration/): Detailed guides for connecting to GitHub, Bitrise, Bitbucket, CircleCI, or any generic CI platform.
3. [Cloud Command Reference](cloud-commands.md): A technical reference for all cloud-specific CLI arguments and parameters.

### Core capabilities

Maestro Cloud provides a purpose-built environment that ensures deterministic results by addressing the common causes of flakiness in mobile testing.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Device Isolation</strong></td><td>Every virtual device is wiped and recreated between tests to ensure complete isolation and repeatability.</td></tr><tr><td><strong>Flexible Configuration</strong></td><td>Customize exact environments, such as Android API levels  or specific iOS models.</td></tr><tr><td><strong>Global Testing</strong></td><td>Test localized app behavior using the <code>--device-locale</code> parameter and fixed regional timezones.</td></tr><tr><td><strong>Cross-Platform</strong></td><td>Native support for Android (Views/Compose), iOS (UIKit/SwiftUI), React Native, Flutter, and Web.</td></tr></tbody></table>

### CI/CD and workflow integration

You can integrate Maestro into your existing development lifecycle. Maestro Cloud offers native integrations with popular CI providers to automate your testing pipeline.

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Native CI Support</strong></td><td>Ready-made integrations for GitHub Actions, Bitrise, Bitbucket Pipelines, and CircleCI.</td></tr><tr><td><strong>Pull Request Integration</strong></td><td>Specifically for GitHub and GitHub Enterprise, Maestro can block merging if test failures are detected in a PR.</td></tr><tr><td><strong>Performance Optimization</strong></td><td>Reuse cached app binaries via the <code>app-binary-id</code> to skip re-uploading the application for every individual test run.</td></tr></tbody></table>

### Next step

Learn [How to run your tests on Maestro Cloud](how-to-run-your-tests-on-maestro-cloud.md) using the tutorial to launch your first parallel test run.
