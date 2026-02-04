---
description: Configure Maestro for Android app testing with emulators or physical devices.
---

# Android

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Maestro provides a high-level abstraction for Android testing by simulating end-user interactions at the presentation layer. Unlike other frameworks, Maestro doesn't live inside your app, it pilots the device from the outside.

### A UI-centric approach

Maestro operates through the Android display stack, ensuring your tests are framework-agnostic. Whether you use Kotlin, Java, Flutter, React Native, or Compose, Maestro interacts only with the rendered UI.

* **Human-Like Simulation**: Maestro translates declarative commands into system-level inputs, mimicking genuine user behavior on the Android input pipeline.
* **Zero Instrumentation**: You don't need to add test dependencies to your `build.gradle` or compile a special "test APK."

### System-level control

Maestro drives the entire device, not just your app. If you need to change Wi-Fi settings, read a notification, create system contacts, or manage anything else that depends on device state, you can do so in exactly the same way a real user would. Check the [how-maestro-works.md](../how-maestro-works.md "mention") for more information.&#x20;

To toggle the system settings, for example, Maestro can navigate to the system drawer or settings to change the environment mid-test.

```yaml
- runScript: "scripts/toggleWifi.js" # Use JS to trigger system intents
- openNotifications
- tapOn: "Airplane mode"
```

Android apps often cache data that can lead to flaky tests. The `clearState` command ensures a reproducible environment by clearing app data (the equivalent of `adb shell pm clear`) before the app launches.

```yaml
- launchApp:
    appId: "com.example.app"
    clearState: true  # Resets app data for a clean launch
```

### Execution and environment setup

Maestro connects to your target via ADB (Android Debug Bridge).

* **Emulators & Physical Devices**: Maestro automatically detects and connects to running emulators or physical devices. For physical hardware, ensure "USB Debugging" is enabled in Developer Options.
* **App Identification**: Maestro targets your application using the **Package Name** found in your `AndroidManifest.xml` (the `appId`).
* **Installation**: Maestro assumes the application is already installed on the target device/emulator before the test begins.

### Cross-platform configuration

Since Android and iOS use different identifiers, we recommend using [Environment variables](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/environment-variables) in your `config.yaml` or [Flows ](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/)to keep them cross-platform.

For example, if you are executing a cross-platform testing that will use different App IDs you can prepare your Flows:

```yaml
# In your Flow
appId: ${APP_ID}
---
- launchApp
```

To run it locally using the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/), just inform the App ID:

```bash
export APP_ID=com.example.android && maestro test flow.yaml
```

### Maestro Cloud

When your suite grows, local sequential execution becomes a bottleneck. [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/) spins up multiple virtual Android devices to run your tests in parallel.

| **Feature**         | **Local Android**  | **Maestro Cloud**                 |
| ------------------- | ------------------ | --------------------------------- |
| **Parallelization** | 1 device at a time | 10+ devices simultaneously        |
| **Speed**           | Slow (Sequential)  | Blazingly Fast (Parallel)         |
| **Cleanup**         | Manual             | Automatic Infrastructure Teardown |

### Next steps

If you already know the Maestro solution you are going to use, access the desired documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)

If you are new to the platform, follow the [QuickStart](../quickstart.md) guide to get up and running in minutes.
