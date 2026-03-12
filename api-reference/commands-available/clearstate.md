---
description: Clear app data, cache, and preferences to reset to fresh install state.
---

# clearState

Clears all data for a specified mobile application.

{% hint style="warning" %}
The `clearState` command is not available for Web.
{% endhint %}

### Usage examples

To clear the state of the current app, use add the `clearState` command alone.

```yaml
- clearState
```

If you want to clear the state of a specific app by its ID, add the app ID:

```yaml
- clearState: app.id
```

Or for a website, when testing on the web platform:

```yaml
- clearState: https://example.com
```

You can also add a `label` when invoking `clearState` to improve the readability of the report.

```yaml
- clearState:
    appId: app.id
    label: Reset ExampleApp
```

### Platform-specific behavior

The command's behavior differs based on the mobile operating system.

{% tabs %}
{% tab title="Android" %}
On Android, the `clearState` command is equivalent to running:

```
adb shell pm clear {package name}
```

It removes all app-related data from the device, such as shared preferences, databases, and accounts.
{% endtab %}

{% tab title="iOS" %}
On iOS, the `clearState` command causes Maestro to reinstall the entire app, resulting in a completely fresh install and removing all existing data folders.

As described in [Stack Overflow](https://stackoverflow.com/a/56746729/7009800) discussion, it's also possible to  `xcrun simctl` to perform the same action.
{% endtab %}

{% tab title="Web" %}
The command clears all browser data (cookies, local storage, etc.) for the [origin](https://developer.mozilla.org/en-US/docs/Glossary/Origin) of the current web app, or of the provided web app URL.
{% endtab %}

{% endtabs %}
