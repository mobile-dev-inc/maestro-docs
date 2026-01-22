# clearKeychain

The `clearKeychain` command clears all data from the iOS Keychain.&#x20;

{% hint style="warning" %}
This command only applies to iOS and has no effect on Android or Web.
{% endhint %}

### Syntax

The command takes no arguments.

```yaml
- clearKeychain
```

### Why use this command?

The iOS Keychain is a secure storage container used by apps to persist login credentials, tokens, and other sensitive information.

In automated testing, the Keychain can become a source of state leakage, where a previous test run leaves a user logged in, causing subsequent tests to fail or behave unexpectedly. Using `clearKeychain` ensures your app starts from a clean, default state.

#### Automate Keychain clearing

If you want to clear the Keychain every time the app starts without adding a separate command, you can use the `clearKeychain` parameter directly within the [`launchApp`](launchapp.md) command:

```yaml
- launchApp:
    clearKeychain: true
```

### Related content

You can use [Hooks](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/hooks) to automate Keychain clearing across all your tests.
