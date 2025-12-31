# Android native

Maestro provides a **black-box testing approach** for native Android applications, contrasting with instrumentation-based frameworks like Espresso or Detox. You write tests in YAML and they execute externally, interacting with the app through accessibility APIs rather than internal instrumentation.

## Key technical advantages

The key technical advantages of using Maestro on Android are:

### Zero instrumentation architecture
- No modifications to source code (Kotlin/Java) required
- No instrumented APK builds or custom gradle configurations
- App testing as a sealed binary through Android accessibility layer
- Eliminates build.gradle test dependency conflicts and compilation overhead

### Accessibility-driven element interaction
Maestro leverages Android's AccessibilityService framework to traverse the view hierarchy:
- Element identification via text matching, `resource-id`, or content-desc attributes
- Commands: `tapOn`, `inputText`, `swipe`, `scroll` interact with native View/Compose trees
- Xpath-like selectors for complex hierarchies
- Supports both View-based (XML layouts) and Jetpack Compose UIs

### App lifecycle management
Configuration via `appId` (package name):

```yaml
appId: com.example.app
```

- APK installation, state clearing (`clearState`), and process termination handled by Maestro command-line tool
- Environment variable substitution for debug/release variants
- Compatible with aab-to-apk conversion in CI pipelines

### APK delivery mechanisms
- **Pre-installed:** Test against existing emulator/device installations
- **Local APK:** Direct path specification for installation before test execution
- **Cloud Upload:** CI integration via Maestro cloud infrastructure

### System-level integration testing
Maestro can interact with Android OS-level components outside app process boundaries:
- Grant/revoke runtime permissions programmatically
- Access system settings, notification drawer, and background processes
- Test app resilience to network loss, permission denials, and system state changes