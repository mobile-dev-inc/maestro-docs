# eraseText

The `eraseText` command deletes characters from the currently focused text field. It behaves like pressing the Backspace key, removing characters, up to 50 characters by default.

### Syntax

You can use the command with no arguments. In this case, it will remove up to 50 characters from the text field.

```yaml
- eraseText # Removes up to 50 characters (default)
```

You also have the option to specify the number of characters to remove, up to a maximum of 100 characters:

```yaml
- eraseText: 100    # Removes up to 100 characters
```

### Known issues

The `eraseText` command can be unreliable on iOS. To ensure that text is cleared consistently, use the following sequence of commands as a workaround:

```yaml
- longPressOn: "<input text id>"
- tapOn: 'Select All'
- eraseText
```

This approach ensures that all text in the input field is selected before executing the erase action.

{% hint style="info" %}
Maestro team is working to fix this issue.
{% endhint %}
