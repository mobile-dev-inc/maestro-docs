---
description: >-
  Detect when your app is running under Maestro automation for test-specific
  behavior.
---

# Detect Maestro

There are times when your application needs to behave differently during a test. Whether you want to bypass a 2FA screen, disable analytics to avoid polluting production data, or point to a mock server, detecting Maestro within your app's code is a common requirement.

### **Why detect Maestro?**

Detecting when your app is under test is a way to handle scenarios that are otherwise difficult to automate:

* **Bypassing 2FA:** Modify authentication flows to use fixed codes, avoiding the need for a physical SIM card or email inbox.
* **Controlling Content Persistence:** Keep short-lived messages (like temporary banners) on the screen longer so Maestro has enough time to detect and interact with them.
* **Environment Switching:** Automatically point your app to a mock server or a staging database to keep production data clean.
* **Disabling Custom Animations:** If your app uses specialized animations that aren't caught by the [`waitForAnimationToEnd`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/waitforanimationtoend), you can turn them off manually to prevent "ghost taps."

### Mobile (iOS and Android)

The gold standard for detecting Maestro on mobile is using [`launchApp arguments`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/launchapp#pass-launch-arguments). This approach is reliable, explicit, and works seamlessly in both local environments and [Maestro Cloud](https://docs.maestro.dev/cloud/run-maestro-tests-in-the-cloud).

{% stepper %}
{% step %}
#### **Pass the argument in your Flow**

In your Maestro Flow, use the `arguments` parameter within the `launchApp` command to send a custom flag.

```yaml
- launchApp:
    appId: "com.example.app"
    arguments:
      isMaestro: "true"
```
{% endstep %}

{% step %}
#### **Detect the argument in your code**

Your application can then check for this flag during its initialization phase.

{% tabs %}
{% tab title="Android (Kotlin/Java)" %}
```kotlin
val isMaestro = intent.getStringExtra("isMaestro") == "true"
if (isMaestro) {
    // Disable analytics or use mock data
}
```
{% endtab %}

{% tab title="iOS (Swift)" %}
```swift
if ProcessInfo.processInfo.arguments.contains("isMaestro") {
    // Apply test-only configurations
}
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
#### Checking for open ports (Deprecated)

In the past, developers checked if ports `7001` (Android) or `22087` (iOS) were open. These were Maestro-specific ports that were used to detect Maestro.

**This method is now deprecated**. It is unsupported in Maestro Cloud and may be removed in future updates. Maestro strongly recommends using the [`launchApp arguments`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/launchapp#pass-launch-arguments) approach.
{% endhint %}
{% endstep %}
{% endstepper %}

### Web

For Web apps, Maestro simplifies detection by injecting a property directly into the global execution context.

Maestro automatically defines `window.maestro` while a test is running. You can check for this property anywhere in your frontend code using `window.maestro`:&#x20;

```javascript
if (window.maestro) {
  console.log("Maestro test is running!");
}
```

#### Related content

* [`launchApp`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/launchapp): Full technical reference for passing launch arguments.
