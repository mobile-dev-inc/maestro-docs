---
description: Configure Maestro for Android app testing with emulators or physical devices.
---

# Android

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Maestro provides a high-level abstraction for Android testing by simulating end-user interactions at the presentation layer. Unlike other frameworks, Maestro doesn't live inside your app, it pilots the device from the outside.

### A UI-centric approach

Maestro operates through the Android display stack, ensuring your tests are framework-agnostic. Whether you use Kotlin, Java, Flutter, React Native, or Compose, Maestro interacts only with the rendered UI.

* **Human-Like Simulation**: Maestro translates declarative commands into system-level inputs, mimicking genuine user behavior on the Android input pipeline.
* **Zero Instrumentation**: You don't need to add test dependencies to your `build.gradle` or compile a special "test APK."

### System-level control

Maestro drives the entire device, not just your app. If you need to change WIFI settings, read a notification, create contacts, or manage anything else that depends on device state or data, you can do so in exactly the same way a real user would, using "real human thumbs."

To manage system settings mid-test, you can interact with the OS directly or use built-in commands:

```yaml
- toggleAirplaneMode
- tapOn: "Airplane mode"
- runFlow: toggle_wifi.yaml # Use a subflow for complex system interactions
```

Android apps often cache data that can lead to flaky tests. The `clearState` command ensures a reproducible environment by clearing app data (the equivalent of`adb shell pm clear <package-name>`) before the app launches, giving the app a "just installed" state.

```yaml
- launchApp:
    appId: "com.example.app"
    clearState: true  # Resets app data for a clean launch
```

### Execution and environment setup

Maestro connects to your target via ADB (Android Debug Bridge).

* **Emulators & Physical Devices**: Maestro automatically detects and connects to running emulators or physical devices. For physical hardware, ensure "USB Debugging" is enabled in Developer Options.
* **App Identification**: Maestro targets your application using the **Package** found in your `AndroidManifest.xml` (the `appId`).
* **Installation**: Maestro assumes the application is already installed on the target device/emulator before the test begins.

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
maestro test -e APP_ID=com.example.android flow.yaml
## or
maestro test --env APP_ID=com.example.android flow.yaml
```

### Maestro Cloud

When your suite grows, local sequential execution becomes a bottleneck. [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/) spins up multiple virtual Android devices to run your tests in parallel.

| **Feature**         | **Local Android**  | **Maestro Cloud**                  |
| ------------------- | ------------------ | ---------------------------------- |
| **Parallelization** | 1 device at a time | Scale to as many devices as needed |
| **Speed**           | Slow (Sequential)  | Blazingly Fast (Parallel)          |
| **Cleanup**         | Manual             | Automatic Infrastructure Teardown  |

### Next steps

Explore the dedicated [Android Native](android-native.md) and [Jetpack Compose](jetpack.md) documentation for platform-specific patterns.

If you already know the Maestro solution you are going to use, access the desired documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)

If you are new to the platform, follow the [QuickStart](../../quickstart.md) guide to get up and running in minutes.
