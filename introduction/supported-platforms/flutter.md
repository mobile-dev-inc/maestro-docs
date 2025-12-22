# Flutter on Maestro

Maestro's approach to Flutter testing embodies an "Arm's Length" methodology, focusing exclusively on device-level automation. Unlike Flutter-specific tools such as Flutter Driver or Integration Test—which inject Dart code and require deep instrumentation within the app process—Maestro interacts with Flutter applications in the same manner as native or React Native apps: by simulating user input and inspecting the final rendered UI.

Flutter Integration Test executes Dart code inside the app's runtime, making tests susceptible to crashes, navigation stack changes, or framework updates that can disrupt test execution. In contrast, Maestro runs externally, orchestrating input events (taps, swipes, text entry) and validating outcomes based on the actual pixels rendered on the device screen. This ensures that tests reflect the true end-user experience, independent of widget tree structure or internal logic.

## Zero explicit framework dependencies

Maestro requires no explicit integration with Flutter or any other UI framework. Its operation is entirely decoupled from the app's internals, relying solely on the device's accessibility and visual output. By driving the device at the OS level, Maestro can automate interactions with any app—Flutter, native, React Native, or web—without knowledge of the underlying architecture or source code.

This framework-agnostic design offers several technical advantages:

- **No maintenance overhead:** Maestro tests remain stable across framework upgrades (e.g., new Flutter or JavaScript releases), as long as the UI layout and accessibility identifiers are consistent.
- **Resilience to app changes:** Since Maestro does not depend on widget tree traversal or internal APIs, changes to app logic or navigation do not break test scripts unless the visual UI itself changes.
- **Broad compatibility:** Maestro can automate system-level flows (notifications, permissions, network changes) that are inaccessible to in-app test frameworks.

This device-centric paradigm delivers robust, future-proof test automation, ensuring that validation is always performed against the actual user-facing interface rather than internal implementation details.

*   **Framework Agnosticism:** Maestro neither connects to Flutter's engine nor traverses the widget tree. It operates at device-level, simulating physical input events and analyzing final visual output.
*   **No Dependencies:** No `pubspec.yaml` integration required. Maestro tests the compiled binary as Android Package (APK) or iOS App Store Package (IPA) directly, whether debug or release builds.

## Cross-platform test unification
Single Flutter codebase for Android and iOS enables single test suite via Maestro.

*   **Platform Abstraction:** Visual interaction commands work identically across platforms if UI layouts remain consistent.
*   **Conditional Logic:** Use environment variables in YAML to handle platform-specific flows such as package IDs and permission dialogs without test duplication.

## Out-of-app interaction
Instrumental Flutter testing can't interact with system-level elements. Maestro operates at OS-level.

*   **Device-Level Automation:** Maestro orchestrates device behavior independent of app process—test push notifications, system settings, network state changes, and verify Flutter's response handling.
