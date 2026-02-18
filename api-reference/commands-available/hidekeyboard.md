---
description: Dismiss the on-screen keyboard if currently visible.
---

# hideKeyboard

The `hideKeyboard` command hides the software keyboard if it is visible.

### Usage examples

The following example hides the keyboard.

```yaml
- hideKeyboard
```

{% hint style="info" %}
This command is a no-op on web. It has no effect when running web tests.
{% endhint %}

{% hint style="success" %}
#### Update

Maestro has updated the `hideKeyboard` command to verify that the keyboard is actually hidden. If the system fails to dismiss the keyboard, the command will now fail the test.

**This behavior is currently only available on Maestro Cloud.** It will be released to Maestro CLI and Maestro Studio soon.
{% endhint %}

### Implementation details

Unlike other UI actions, mobile operating systems do not provide a native way for closing the keyboard. To achieve this, Maestro simulates the specific gestures or actions a user would perform on each platform:

* **Android**: Maestro triggers a back button event, which is the standard system-level action to dismiss an active keyboard. This is identical to the [back.md](back.md "mention") command.
* **iOS**: Since iOS does not have a back button, Maestro performs small, quick swipes in the middle of the screen to trigger the system's auto-hide behavior.

### Workarounds

Because the Maestro implementation methods rely on system behaviors rather than direct APIs, they can occasionally be affected by specific app layouts or keyboard types.

If the keyboard doesn't hide, a reliable workaround is to use the `tapOn` command to click a non-tappable element on the screen (such as a header, a title bar, or an empty background area). This mimics how a user might dismiss the keyboard.

```yaml
- tapOn:
    id: "header_title" # Tap on a safe area to force the keyboard down
```
