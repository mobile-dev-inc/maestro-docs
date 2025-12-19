# React Native testing with Maestro

Maestro provides robust end-to-end testing capabilities for **React Native** applications. Through its black-box approach and remote execution model, Maestro interacts with the rendered UI layer rather than the JavaScript bridge or internal framework implementation.

This makes Maestro the preferred choice for React Native teams, including **Meta's React Native team**, which uses Maestro for framework core testing.

## Technical architecture

Maestro operates at the accessibility layer with UIAccessibility on iOS and AccessibilityService on Android, simulating user gestures on the rendered interface. Unlike instrumentation-based frameworks such as Detox and Appium, Maestro requires no code injection, runtime modifications, or special build configurations.

## Zero-configuration paradigm

Unlike traditional frameworks requiring explicit configuration or debug builds, Maestro operates without React Native-specific setup:

*   **Framework Agnostic:** Maestro instruments the device at the OS level, simulating finger touches. It's indifferent to whether UI elements render via React Native, Flutter, or native code.
*   **Production Binaries:** Test identical Android Package (APK) and iOS App Store Package (IPA) artifacts distributed to app stores without instrumenting or repackaging.

## Cross-platform testing strategy for Android and iOS

Maestro enables single-source test automation across platforms using **YAML-based flow definitions** compatible with both iOS and Android.

### Platform-specific configuration

Handle divergent app identifiers with `com.app` on Android versus `com.app.ios` on iOS using environment variable substitution:

```yaml
appId: ${APP_ID}
---
- launchApp
```

Invoke with platform-specific values:

```bash
APP_ID=com.app maestro test flow.yaml  # Android
APP_ID=com.app.ios maestro test flow.yaml  # iOS
```

## Element selection and test IDs

While Maestro prioritizes visible text matching, React Native's `testID` prop enables robust element targeting:

*   **React Native Implementation:** Add `testID="element_id"` to components
*   **Native Mapping:** Automatically mapped to `resource-id` for Android and `accessibilityIdentifier` for iOS
*   **Maestro Query:** Maestro resolves these identifiers, decoupling tests from dynamic text content

## JavaScript execution

Maestro supports inline JavaScript for complex test logic:

```yaml
- runScript: |
    return Math.random().toString(36).substring(7)
```

*   **Restricted Sandbox:** Isolated JS environment without file system or external module access
*   **Use Cases:** Dynamic test data generation, conditional assertions, payload manipulation

## Advanced patterns

*   **Deep Linking:** Use `openLink` to trigger URL-based navigation routes
*   **Accessibility Considerations:** Maestro respects standard React Native accessibility APIs; ensure interactive elements have appropriate accessibility traits
*   **Performance Profiling:** Combine with React Native DevTools for render cycle analysis during test execution
