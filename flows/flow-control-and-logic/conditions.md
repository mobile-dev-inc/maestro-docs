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

| Condition    | Description                                                                                                                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `visible`    | Executed if the element matching the selector is visible. The element must be defined using one or more [Selectors](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors "mention").          |
| `notVisible` | Executed if the element matching the selector is **not** visible. The element must be defined using one or more  [Selectors](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors "mention"). |
| `platform`   | Executed if the current platform matches (`Android`, `iOS`, or `Web`).                                                                                                                            |
| `true`       | Executed if the JavaScript expression evaluates to `true`.                                                                                                                                        |

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

Sometimes an element may or may not appear, such as a "Rate this App" popup or a newsletter signup. You can handle these dynamic states using two different patterns:

{% tabs %}
{% tab title="The runFlow / when block" %}
This is the most idiomatically expressive way to handle conditions. It clearly defines the intent "Only run these commands _when_ this condition is met." You combine [`runFlow`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/runflow) and `when`:&#x20;

```yaml
- runFlow:
    when:
      visible: "Dismiss"
    commands:
      - tapOn: "Dismiss"
```
{% endtab %}

{% tab title="The optional property" %}
Using the `optional` property is simpler for single-command interactions. It allows the step to fail without failing the entire test.&#x20;

```yaml
- tapOn:
    text: "Dismiss"
    optional: true
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Relying on unstable UI states for conditions can lead to flaky tests. Ensure your `visible` selectors are unique and reliable.
{% endhint %}

#### Using `notVisible` for negative conditions

You can use the `notVisible` condition to handle inverse or “else” scenarios where an action should occur only when a specific element is _not_ present on the screen.

For example, the following command taps **Standard Login** only if the **Biometric Login** option is not visible. The `runFlow` command is used here because the `tapOn` command itself does not support conditional logic:

```yaml
- runFlow:
    when:
      notVisible: "Biometric Login"
    commands:
      - tapOn: "Standard Login"
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

If your JavaScript condition is longer than one line, move the logic into a separate `.js` file and use the `output` variable to keep your YAML clean.&#x20;

The following example shows how to move the logic to an external file. First, create your script logic:

```javascript
// checkFeature.js
output.shouldRunTest = (MAESTRO_PLATFORM === 'Android' && someComplexCalculation() > 10);
```

Then, reference it in your Flow:

```yaml
- runScript: checkFeature.js
- runFlow:
    when:
      true: ${output.shouldRunTest}
    file: subflows/advanced-test.yaml
```

#### Next steps

Now that you understand how to use conditions in your Flows, learn how to use [parameters and constants](parameters-and-constants.md) or explore all the possibilities of using [JavaScript](../javascript/javascript-overview.md) to create tests.
