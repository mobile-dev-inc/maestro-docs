# Hooks

In automated testing, you often need to perform specific setup or cleanup tasks for every test. Instead of manually adding a `runFlow` to the start or end of every file, Maestro provides Hooks.

Hooks allow you to define global logic that executes automatically at specific lifecycle points of your test suite. This ensures a consistent environment, reduces boilerplate code, and simplifies maintenance.

#### Types of Hooks

Maestro supports two primary hooks defined in your `config.yaml`. These hooks are workspace-wide, meaning they apply to every Flow within that directory.

<table data-header-hidden><thead><tr><th width="152.33334350585938"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Hook</strong></td><td><strong>When it runs</strong></td><td><strong>Ideal Use Case</strong></td></tr><tr><td><code>onFlowStart</code></td><td>Before every individual Flow begins.</td><td>Resetting app state, logging in, or handling dynamic permissions.</td></tr><tr><td><code>onFlowComplete</code></td><td>After every individual Flow finishes (Pass or Fail).</td><td>Clearing cookies, logging out, or reporting custom metrics.</td></tr></tbody></table>

#### Usage example

Let's walk through how to set up a global login hook so that every test in your workspace starts with an authenticated user.

**Step 1: Create your login subflow**

Create a reusable file at `subflows/login.yaml`. This is a standard Flow file.

```yaml
# subflows/login.yaml
appId: com.example.app
---
- launchApp
- tapOn: "Username"
- inputText: "maestro_user"
- tapOn: "Login"
```

**Step 2: Register the hook in `config.yaml`**

Open the `config.yaml` file in your workspace root. Use the `hooks` block to point to your login subflow.

```yaml
# config.yaml
appId: com.example.app

hooks:
  onFlowStart: 
    runFlow: subflows/login.yaml
```

**Step 3: Run your tests**

Now, when you run any test in your folder using `maestro test .`, Maestro will execute the `login.yaml` sequence before starting the logic in your specific test file.

#### Advanced: Dynamic Hooks

You can pass environment variables into your hooks just like a standard `runFlow`. This is useful for switching roles (e.g., User vs. Admin) across your entire suite.

```yaml
# config.yaml
hooks:
  onFlowStart:
    runFlow:
      file: subflows/login.yaml
      env:
        ROLE: "admin"
```

#### Best Practices & Tips

* Keep Hooks Lean: Since hooks run for every single Flow, a slow hook will significantly increase your total suite execution time.
* Avoid Infinite Loops: Be careful not to call a Flow that itself triggers the same hook.
* Conditional Hooks: Use the `when` block within your hook sub-flow to perform actions only on specific platforms (e.g., clearing the iOS Keychain).
* Cleanup with `onFlowComplete`: Use this hook to ensure your app is in a "neutral" state for the next test, such as navigating back to the home screen or logging out.

#### Related Documentation

* [Nested Flows](https://www.google.com/search?q=nested-flows): Understand the underlying `runFlow` command used by hooks.
* [Sequential Execution](https://www.google.com/search?q=sequential-execution): Learn how hooks interact when running tests in a specific order.
* [Parameters and Constants](https://www.google.com/search?q=parameters-and-constants): See how to manage variables within your hooks.

Would you like me to create the "JavaScript Overview" page next to show how you can use logic to make your hooks even more powerful?
