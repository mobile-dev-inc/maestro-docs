---
hidden: true
---

# Page

Maestro provides a high-level abstraction for Android testing by simulating end-user interactions at the presentation layer. Unlike other frameworks, Maestro doesn't live inside your app, it pilots the device from the outside.

### A UI-centric approach

Maestro operates through the Android display stack, ensuring your tests are framework-agnostic. Whether you use Kotlin, Java, Flutter, React Native, or Compose, Maestro interacts only with the rendered UI.

* **Physical Input Simulation**: Every command is translated into a native `MotionEvent`. When you say `tapOn`, Maestro triggers the same input pipeline a human thumb would.
* **Zero Instrumentation**: You don't need to add test dependencies to your `build.gradle` or compile a special "test APK."

### System-level control

Maestro’s [Arm's Length](../how-maestro-works.md) architecture means it can control the entire Android OS, allowing you to test scenarios that happen _outside_ your app boundaries.

To toggle the system settings, for example, Maestro can navigate to the system drawer or settings to change the environment mid-test.

```yaml
- runScript: "scripts/toggleWifi.js" # Use JS to trigger system intents
- openNotifications
- tapOn: "Airplane mode"
```

When testing, Android apps often cache data that makes tests flaky. The `clearState` command is your most powerful tool for reproducibility, since you will start with a clean launch.&#x20;

```yaml
- launchApp:
    appId: "com.example.app"
    clearState: true  # Uninstalls and reinstalls the APK automatically
```

### Execution and environment setup

Maestro connects to your target via ADB (Android Debug Bridge).

* **Emulators**: Ensure your emulator is running. Maestro looks for the `ro.kernel.qemu` property to detect the virtual environment.
* **Physical Devices**: Enable "USB Debugging" in Developer Options. Maestro handles the agent installation automatically.
* **App Identification**: Use the Package Name found in your `AndroidManifest.xml`.

### Platform-specific configuration

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

When your suite grows, local sequential execution becomes a bottleneck. [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/) spins up multiple Android virtual devices to run your tests in parallel.

| **Feature** | **Local Android**  | **Maestro Cloud**                 |
| ----------- | ------------------ | --------------------------------- |
| Concurrency | 1 device at a time | 10+ devices simultaneously        |
| Speed       | Slow (Sequential)  | Blazingly Fast (Parallel)         |
| Cleanup     | Manual             | Automatic Infrastructure Teardown |

###
