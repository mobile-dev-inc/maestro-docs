# hideKeyboard

The `hideKeyboard` command hides the software keyboard if it is visible.

{% hint style="warning" %}
#### Unreliable command for iOS

On iOS, `hideKeyboard` is done with the help of scrolling up and down from the middle of the screen since there is no native API to hide the keyboard. This behavior can be flaky.

If the `hideKeyboard` command does not hide the keyboard, use the `tapOn` command to click a non-tappable region, similar to how a user would hide the keyboard manually.
{% endhint %}

### Usage examples

The following example hides the keyboard.

```yaml
- hideKeyboard
```
