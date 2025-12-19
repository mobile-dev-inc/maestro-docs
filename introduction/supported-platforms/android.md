# Android

Maestro provides a high-level abstraction for Android testing by simulating end-user interactions at the presentation layer rather than through internal APIs or framework hooks.

### UI-centric testing approach
Maestro operates through the Android display stack, treating the device as a black box.
*   **Framework Agnostic:** Tests work regardless of implementation details—Kotlin, Java, Flutter, React Native, or Compose. Maestro interacts with rendered UI elements, not the view hierarchy.
*   **Physical Input Simulation:** Maestro translates declarative commands into actual tap events (MotionEvent) and system inputs, mimicking genuine user behavior on the Android input pipeline.

### System-level instrumentation
Maestro can control the entire device, not just the target app.
*   **System Integration:** Tests can navigate outside the app (for example, Settings, system dialogs), modify device state (Wi-Fi, locale, notifications), and verify behavioral changes. This is particularly useful for permission flows and system integration scenarios.
*   **State Management:** The `clearState` command uninstalls and reinstalls the APK, ensuring a clean state between test runs and reproducible test environments.

### Execution environment setup
Tests execute on Android emulators or physical devices via the Maestro agent.
*   **Emulator Integration:** Maestro connects via ADB (Android Debug Bridge) to running emulator instances. The device must have `ro.kernel.qemu` property or equivalent for proper detection.
*   **APK Installation:** Maestro handles APK deployment via `adb install`. Specify the APK path in your configuration, or target pre-installed apps by package name.
*   **App Launch:** Define `appId` (package name, for example, `com.example.app`) to target the correct app process.

### Platform-specific configuration
While YAML syntax unifies across platforms, Android-specific identifiers differ from iOS.
*   **Environment Variables:** Use environment substitution for `appId` to support both platforms. For example, `${ANDROID_APP_ID}` resolves at runtime based on the target platform.

### Maestro cloud execution
Maestro cloud distributes Android tests across device farms.
*   **Parallelization:** Tests execute in parallel across available virtual devices, reducing feedback latency for large test suites.