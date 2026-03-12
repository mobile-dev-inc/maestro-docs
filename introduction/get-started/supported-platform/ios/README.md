---
description: >-
  Black-box iOS testing via the Accessibility layer. Run on Xcode Simulators,
  handle permissions, test multi-app journeys, and parallelize with Cloud.
---

# iOS

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Maestro provides a high-level abstraction for iOS testing by simulating end-user interactions at the presentation layer. Unlike traditional testing tools that require deep instrumentation, Maestro interacts with the iOS Accessibility layer, allowing you to test your app exactly as a user would.

### Black-box approach

Maestro analyzes the rendered frames of the iOS device, ensuring your tests are framework-agnostic. Whether your app is built with Swift, Objective-C, Flutter, React Native, or SwiftUI, Maestro interacts only with the visual output.

* **Physical Input Simulation**: Declarative commands are translated into native touch events. When you use `tapOn`, Maestro triggers the same iOS input pipeline that a physical touch would.
* [**Arm's Length**](../../how-maestro-works.md): Maestro doesn't require access to your source code or bytecode. You test the same `.app` bundle (the Simulator version) that runs on your virtual testing environment.

### System-level control

Maestro’s architecture allows it to pilot the entire device, not just your application process. This enables testing for complex real-world scenarios.

iOS is known for its strict permission dialogs (Location, Camera). However, Maestro can interact with these system prompts directly:

```yaml
- launchApp:
    appId: "com.example.app"
    permissions:
      location: allow
      notifications: allow
```

Maestro also allows you to create multi-app journeys. You can test flows that leave your app, such as opening a link in Safari or checking an email, and then return to your application:

```yaml
- tapOn: "Open Website"
# Maestro follows the link into Safari
- assertVisible: "Welcome to our site"
- tapOn:
    id: "breadcrumb" # Native iOS 'Back' button to return to your app
```

### Execution and environment setup

Maestro connects to your target via native Apple development tools.

* **Simulators**: Run tests on any iOS Simulator managed by Xcode. Ensure you have the Xcode Command Line Tools installed (`xcode-select --install`).
* **App Identification**: iOS apps are targeted using the Bundle ID (e.g., `com.example.app`).

### Cross-platform configuration

If your Android and iOS applications use different identifiers, we recommend using [environment variables](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants) to keep your [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) cross-platform.

You can manage these variables in three primary ways:

1. **Maestro Studio**: Configured via the [Environment Manager](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/environments-and-variables).
2. [**Maestro CLI**](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants#passing-parameters-via-cli): Passed as arguments during execution.
3. **Flow Configuration**: Defined directly in the [config matter](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants#constants) at the top of an individual Flow file.

To run a single test suite against different platforms where the App ID varies, structure your Flow to use a variable:

```yaml
# In your Flow
appId: ${APP_ID}
---
- launchApp
```

When executing locally with the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/), use the `-e` or `--env` flag to inject the correct identifier for that specific run:

```bash
maestro test -e APP_ID=com.example.app.ios flow.yaml
## or
maestro test --env APP_ID=com.example.app.ios flow.yaml
```

### Parallelization for iOS

Scaling iOS tests locally can be difficult due to macOS hardware requirements. [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/readme) provides instant access to a fleet of iOS Simulators, allowing you to run your entire suite in parallel.

* **Speed**: Reduce test time drastically.
* **Reliability**: Eliminate "flaky" results caused by local machine resource contention.
* **CI/CD Integration**: Automatically trigger parallel iOS runs on every Pull Request.

### Next steps

Explore the dedicated [UIKit](uikit.md) or [SwiftUI](swiftui.md) documentation, or access the [QuickStart](../../quickstart.md) guide to get up and running in minutes if you do not know how to create tests with Maestro.

If you already know which Maestro solution you are going to use, access the relevant documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/readme)
