# iOS testing with Maestro

Maestro provides robust automation support for iOS, maintaining the same "black-box" philosophy applied to Android. Whether the app is built natively (Swift/Objective-C) or via cross-platform frameworks (React Native, Flutter), Maestro interacts with the iOS Simulator or physical devices by simulating genuine user interactions through the Accessibility layer and computer vision.

## "Arm's length" architecture on iOS

Maestro operates on iOS following the *extreme arm's length* principle:

* **Code Independence:** Maestro doesn't require access to iOS source code, bytecode inspection, or app instrumentation. It's agnostic to UI frameworks (UIKit, SwiftUI, or hybrid implementations).
* **Computer Vision:** The framework analyzes rendered frames from the iOS Simulator via XCTest or physical devices via WebDriverAgent. If an element is visually detectable, Maestro can interact with it, ensuring tests validate actual user experience.

## Unified YAML syntax

Maestro's test syntax is platform-agnostic. Commands like `tapOn: "Login"` execute identically across iOS and Android.

* **Code Reuse:** Teams using React Native or Flutter can often reuse the **same test file** across both platforms, reducing maintenance overhead.

## Bundle ID management with environment variables

Platform-specific app identifiers require careful handling:

* **iOS vs. Android IDs:** Android uses *Package Name* (for example, `com.example.app`), while iOS uses *Bundle ID* (for example, `com.example.app.ios`).
* **Solution:** Use **environment variables** in your test files: `${APP_ID}`. Set the appropriate identifier at runtime based on target platform and build variant.

## System-level interaction

Maestro controls the **device**, not just the app process:

* **System Dialogs:** Native iOS permission prompts (location, notifications, camera) are directly accessible and automatable.
* **Settings Integration:** Tests can navigate to the iOS Settings app, modify configurations, and return to your app to verify behavioral changes.

## Execution: local and cloud

* **Local:** Run tests via Maestro command-line tool or Studio connected to an iOS Simulator on macOS (or physical device with proper provisioning).
* **Maestro cloud:** Leverage cloud infrastructure for parallel iOS test execution across multiple simulator instances, eliminating local device management complexity.