---
description: Set the device clipboard content to a specified text value.
---

# setClipboard

The `setClipboard` command sets a specified text string to Maestro's in-memory clipboard. It allows you to define the clipboard content directly, unlike `copyTextFrom` which copies text from a UI element.

### Syntax

The `setClipboard` command accepts a string or a JavaScript expression:

```yaml
- setClipboard: "custom@example.com"  # string
- setClipboard: "${'user' + Math.floor(Math.random() * 1000) + '@example.com'}" # JavaScript expression
```

### Usage examples

#### Set a static value

This example sets a static email address to the clipboard and then pastes it into a text field instead of typing. Using [`pasteText`](pastetext.md) can help avoid flakiness when entering text.

```yaml
appId: com.example.app
---
- launchApp
- tapOn:
    id: "emailField"
- setClipboard: "custom@example.com"
- pasteText
```

#### Set a dynamic value

You can use a JavaScript expression to generate dynamic content for the clipboard.

```yaml
appId: com.example.app
---
- launchApp
- setClipboard: ${'user' + Math.floor(Math.random() * 1000) + '@example.com'}
- tapOn:
    id: "emailField"
- pasteText
```

#### Access clipboard contents

You can access the clipboard's contents in subsequent steps using the `maestro.copiedText` property.

```yaml
appId: com.example.app
---
- setClipboard: "test@example.com"
- inputText: ${'Email: ' + maestro.copiedText}
```

### Related commands

* [pastetext.md](pastetext.md "mention")
* [copytextfrom.md](copytextfrom.md "mention")

