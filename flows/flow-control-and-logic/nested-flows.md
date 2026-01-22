# Nested flows

As your test suite grows, you'll find that certain sequences of commands are repeated across multiple flows. Common examples include logging in, clearing app state, or navigating to a specific screen.

Instead of duplicating these commands in every file, you can define them once in a separate flow and run them using the [`runFlow` ](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/runflow)command. This approach, known as nesting flows, helps you adhere to the DRY (Don't Repeat Yourself) principle, making your tests easier to read, maintain, and optimize.

### Basic Usage

To run a subflow, use the `runFlow` command followed by the path to the flow file.

In this example, the `login.yaml` subflow handles the entire login process for the Wikipedia Android app, including launching the app and navigating the menu. The main flow `profile_test.yaml` runs this subflow to authenticate before performing other checks.

{% tabs %}
{% tab title="tests/profile_test.yaml (The main flow)" %}
```yaml
appId: org.wikipedia
---
- launchApp
- runFlow: ../common/login.yaml 
- assertVisible: "Explore"
```
{% endtab %}

{% tab title="common/login.yaml (The subflow)" %}
```yaml
appId: org.wikipedia
---
- tapOn:
    id: drawer_icon_menu
- tapOn: LOG IN / JOIN WIKIPEDIA
- tapOn: Username
- inputText: myUsername
- tapOn: Password
- inputText: myPassword
- tapOn: LOG IN
```
{% endtab %}
{% endtabs %}

### Passing Arguments

You can make your nested flows dynamic by passing arguments. This allows you to reuse the same logic with different data, such as logging in with different user roles.

Use the `env` key to pass variables to the subflow. Inside the subflow, you can access these variables using the `${VAR_NAME}` syntax.

{% tabs %}
{% tab title="tests/profile_test.yaml (The main flow)" %}
```yaml
appId: org.wikipedia
---
- launchApp
- runFlow:
    file: ../common/login.yaml
    env:
        USERNAME: "myUser"
        PASSWORD: "myPassword"
- assertVisible: "Explore"
```
{% endtab %}

{% tab title="common/login.yaml (The subflow)" %}
```yaml
appId: org.wikipedia
---
- tapOn:
    id: drawer_icon_menu
- tapOn: LOG IN / JOIN WIKIPEDIA
- tapOn: Username
- inputText: ${USERNAME}
- tapOn: Password
- inputText: ${PASSWORD}
- tapOn: LOG IN
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### Conditional execution

You can optimize your test execution by running nested flows only when specific conditions are met.

To learn more about conditional execution, access the [Conditions ](conditions.md)page.
{% endhint %}

### Best Practices for Optimization

Adopting a nested flow strategy directly contributes to an optimized testing process.

#### Keep flows atomic

Each nested flow should perform a single, well-defined task. For example, have separate flows for `login.yaml`, `logout.yaml`, and `onboarding.yaml`. This granular approach allows you to mix and match flows to create complex test scenarios without unnecessary overhead.

#### Organized directory structure

Maintain a clean project structure by grouping reusable flows. A common pattern is to have a `subflows/` or `common/` directory separate from your main test cases.

```
.
├── flows/
│   ├── e2e/
│   │   ├── checkout_flow.yaml
│   │   └── profile_flow.yaml
│   └── subflows/
│       ├── login.yaml
│       └── payment_setup.yaml
```

#### Setup and teardown

Use nested flows for setup and teardown routines. By isolating these steps, you can quickly adjust the initial state for all tests by modifying a single file. For instance, if the login UI changes, you only need to update `subflows/login.yaml`, and all tests using it will automatically work.

### Next steps

Check the [runFlow ](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/runflow)command for technical details, or explore [Conditions](conditions.md) to add logic to your flows.
