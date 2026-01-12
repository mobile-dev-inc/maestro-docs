# Supported platforms

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Maestro operates on the principle of UI-layer automation rather than code instrumentation. Like a test driver interacting with any vehicle through its controls (steering wheel, pedals), Maestro interfaces with applications through their visual and accessibility layers, regardless of the underlying technology stack.

### Mobile operating systems (core)

Maestro provides comprehensive automation support for major mobile platforms:

* **Android:** Full support for emulators and physical devices (API level 21+).
* **iOS:** Full support for simulators and physical devices (iOS 11.0+).

Both platforms pass validation at scale by enterprise teams at Microsoft, DoorDash, and others for complex automation scenarios.

### Framework agnosticism

Maestro decouples test automation from framework implementation through UI-layer interaction, eliminating dependency on framework-specific instrumentation (unlike Detox or Appium with native drivers).

Supported technology stacks include:

* **Native:** Swift, Kotlin, Java, Objective-C.
* **Cross-platform:** React Native, Flutter.
* **Other hybrid frameworks.**

**Technical Implementation:** Maestro synthesizes tap events and leverages the accessibility hierarchy (UIAccessibility/AccessibilityNodeProvider) for element detection, making framework choice irrelevant to test execution.

### Web automation

* **Status:** Functional with ongoing development.
* **Approach:** Maestro extends support to web applications, enabling cross-platform test consolidation using consistent automation syntax.
* **Use Case:** Unified testing strategy across mobile and web surfaces.

### System-level interaction

Maestro supports device-level automation beyond app boundaries:

* **System Interaction:** Navigate to Settings, modify permissions, toggle Wi-Fi, and monitor app behavior in response to system state changes.
* **Real-world Scenarios:** Automated testing of notification handling, permission flows, and inter-app interactions.

### Next steps

Explore the details on how to use Maestro in each one of the supported operating systems and frameworks:

* [android.md](android.md "mention")
* [android-native.md](android-native.md "mention")
* [ios.md](ios.md "mention")
* [flutter.md](flutter.md "mention")
* [web-browser.md](web-browser.md "mention")
* [jetpack.md](jetpack.md "mention")
* [swiftui.md](swiftui.md "mention")
* [uikit.md](uikit.md "mention")
