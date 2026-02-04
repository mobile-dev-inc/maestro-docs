---
description: Paste text from clipboard into the currently focused input field.
---

# pasteText

The `pasteText` command pastes text from the clipboard into the currently focused UI element.

This command requires that a text field is in focus before execution. Text must first be copied to the clipboard using the [`copyTextFrom` ](copytextfrom.md)command.

{% hint style="info" %}
#### System vs. internal clipboard

Maestro distinguishes between two types of clipboards:

* **Internal clipboard**: Stores text captured by Maestro commands, such as `copyTextFrom`, or values manually assigned to `maestro.copiedText`.
* **System clipboard**: The native operating system clipboard used when interacting with in-app actions like a **Copy to Clipboard** button.

The `pasteText` command interacts **exclusively** with Maestro’s internal clipboard. It does not read from or write to the system clipboard.

As a result, if you tap a button in your app that copies content to the system clipboard, `pasteText` will not paste that content. It will only paste text that was previously captured using `copyTextFrom` or explicitly assigned to `maestro.copiedText`.
{% endhint %}

### Syntax

This command takes no arguments.

```yaml
- pasteText
```

### Usage examples

The following example copies text from an element with the ID `someId`, taps a search field to give it focus, and then pastes the copied text into it.

```yaml
appId: com.example.app
---
- launchApp
- copyTextFrom:
    id: "someId"
- tapOn:
    id: "searchFieldId"
- pasteText
```

### Related commands

* [copytextfrom.md](copytextfrom.md "mention")
