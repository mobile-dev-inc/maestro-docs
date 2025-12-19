# Flutter on Maestro

Maestro's support for Flutter exemplifies the framework's "Arm's Length" philosophy. Unlike Flutter-specific testing tools such as Flutter Driver and Integration Test requiring deep instrumentation, Maestro interacts with Flutter apps identically to native or React Native apps: through visual UI inspection.

Flutter Integration Test executes Dart code within the app process—crashes or native navigation breaks test control. Maestro executes external scripts simulating a technology-agnostic user, interacting purely with rendered UI elements. This validates actual UX rather than widget logic.

## Zero explicit framework support

> **Maestro's core technical principle**: "Maestro need not support Flutter explicitly because it only supports what renders on-screen."

*   **Framework Agnosticism:** Maestro neither connects to Flutter's engine nor traverses the widget tree. It operates at device-level, simulating physical input events and analyzing final visual output.
*   **No Dependencies:** No `pubspec.yaml` integration required. Maestro tests the compiled binary as Android Package (APK) or iOS App Store Package (IPA) directly, whether debug or release builds.

## Visual and semantic interaction
Flutter renders via Skia/Impeller rasterization. Maestro leverages optical character recognition (OCR) and native accessibility hierarchies for interaction.

*   **Text Recognition:** Reference visible text for interaction.
    *   Command: `tapOn: "Login"`
    *   Mechanism: OCR locates rendered text coordinates and simulates tap input.
*   **Accessibility Semantics:** For non-text elements, Maestro relies on Android and iOS native accessibility trees exposed by Flutter's `Semantics` widget.
    *   **Implementation:** Apply `Semantics` wrappers or `semanticsLabel` properties to ensure elements are discoverable via Maestro Studio's accessibility inspector.

## Cross-platform test unification
Single Flutter codebase for Android and iOS enables **single test suite** via Maestro.

*   **Platform Abstraction:** Visual interaction commands work identically across platforms if UI layouts remain consistent.
*   **Conditional Logic:** Use environment variables in YAML to handle platform-specific flows such as package IDs and permission dialogs without test duplication.

## Out-of-app interaction
Instrumental Flutter testing can't interact with system-level elements. Maestro operates at OS-level.

*   **Device-Level Automation:** Maestro orchestrates device behavior independent of app process—test push notifications, system settings, network state changes, and verify Flutter's response handling.
