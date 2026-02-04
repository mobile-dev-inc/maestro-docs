---
description: >-
  Execute commands conditionally based on visibility, platform, or custom
  expressions.
---

# Conditions

Conditions allow you to execute commands or entire Flows only when specific criteria are met. This is useful for handling platform-specific logic (Android vs. iOS vs. Web), managing A/B tests, or dealing with dynamic UI elements like onboarding screens or permission dialogs.

{% hint style="success" %}
#### Keep your tests simple

Overusing conditional logic can make your Flows hard to read and debug. Prefer separate Flows for significantly different scenarios.
{% endhint %}

### Supported conditions

In Maestro, conditions are primarily handled using the `when` argument. It can be attached to several commands. If the condition inside the `when` block evaluates to `true`, Maestro executes the command; otherwise, Maestro simply skips that command and moves on to the next one.

The following table lists the available conditions you can use to define the conditional execution of your Flow.

<table><thead><tr><th width="129">Condition</th><th>Description</th></tr></thead><tbody><tr><td><code>visible</code></td><td>Executed if the element matching the selector is visible. The element must be defined using one or more <a data-mention href="https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors">Selectors</a>.</td></tr><tr><td><code>notVisible</code></td><td>Executed if the element matching the selector is <strong>not</strong> visible. The element must be defined using one or more <a data-mention href="https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors">Selectors</a>.</td></tr><tr><td><code>platform</code></td><td>Executed if the current platform matches (<code>Android</code>, <code>iOS</code>, or <code>Web</code>).</td></tr><tr><td><code>true</code></td><td>Executed if the JavaScript expression evaluates to <code>true</code>.</td></tr></tbody></table>

### Common use cases

#### Handling platform differences

Mobile apps often have different UI or behaviors on Android, iOS, or Web. You can use the `platform` condition to run platform-specific Flows.

In this example, the test executes a specific subflow to handle permissions, depending on whether the device is running Android, iOS, or Web.&#x20;

```yaml
- runFlow:
      when:
      platform: Android
    file: subflows/android-permissions.yaml

- runFlow:
    when:
      platform: iOS
    file: subflows/ios-permissions.yaml
    
- runFlow:
    when:
      platform: Web
    file: subflows/web-permissions.yaml
```

#### Handling dynamic state

Sometimes an element may or may not appear, such as a "Rate this App" popup or a newsletter signup. You can use `visible` to handle these dynamic states without failing the test if the element is missing.

In this example, the **Dismiss** button is tapped only if it is currently visible on the screen.

```yaml
- runFlow:
    when:
      visible: "Dismiss"
    commands:
      - tapOn: "Dismiss"
```

The same result can be achieved by using the condition directly with the `tapOn` command:

```yaml
- tapOn: "Dismiss"
  when:
    visible: "Dismiss"
```

{% hint style="success" %}
Relying on unstable UI states for conditions can lead to flaky tests. Ensure your `visible` selectors are unique and reliable.
{% endhint %}

#### Using `notVisible` for negative conditions

You can use the `notVisible` condition to handle inverse or “else” scenarios, cases where an action should occur only when a specific element is _not_ present on the screen.

For example, the following command taps **Standard Login** only if the **Biometric Login** option is not visible:

```yaml
- tapOn: "Standard Login"
  when:
    notVisible: "Biometric Login"
```

This approach allows your tests to adapt to different UI states.

#### Running multiple commands

You don't always need to create a separate file for conditional steps. You can use the `commands` list to define multiple actions inline.

In this example, if the "Welcome to our App" text is visible, the flow executes a sequence of taps to navigate through the onboarding screen.

```yaml
- runFlow:
    when:
      visible: "Welcome to our App"
    commands:
      - tapOn: "Next"
      - tapOn: "Get Started"
```

#### Multiple conditions

You can combine multiple conditions in a single `when` block. Note that all conditions must be met (AND logic) for the commands to execute.

In this example, the **Allow** button is tapped only if the platform is Android AND the **Allow Notifications** text is visible.

```yaml
- runFlow:
    when:
      platform: Android
      visible: "Allow Notifications"
    commands:
      - tapOn: "Allow"
```

#### Advanced logic with JavaScript

For more complex logic, such as feature flags or checking variables, use the `true` condition with a JavaScript expression.

In this example, the `new-feature-test.yaml` subflow is executed only if the `IS_FEATURE_ENABLED` variable evaluates to true.

```yaml
- runFlow:
    when:
      true: ${IS_FEATURE_ENABLED == true}
    file: subflows/new-feature-test.yaml
```

{% hint style="success" %}
If your JavaScript condition is longer than one line, move the logic into a separate `.js` file and use the `output` variable to keep your YAML clean.
{% endhint %}

#### Next steps

Now that you understand how to use conditions in your Flows, learn how to use [parameters](parameters-and-constants.md) and [constants](/broken/pages/DLtBiFLCJpsE4uxGnPNx) or explore all the possibilities of using [JavaScript](../javascript/javascript-overview.md) to create tests.
