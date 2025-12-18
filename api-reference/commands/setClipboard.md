---
description: >-
  Set text directly to Maestro's clipboard (maestro.copiedText) for reuse in tests or
  scripts. This complements copyTextFrom which copies text from UI elements.
---

# setClipboard

You can set text directly to Maestro's clipboard and save it in-memory, to paste later. Unlike `copyTextFrom` which copies text from UI elements, `setClipboard` allows you to specify the text directly.

### Usage Example

This command is useful when you want to avoid input flakiness by pasting text instead of typing:

```yaml
appId: com.example.app
---
- launchApp
- tapOn:
    id: "emailField"
- setClipboard: "custom@example.com"
- pasteText
```

### Related Commands

- [`pasteText`](./pastetext.md) - Paste the clipboard contents
- [`copyTextFrom`](./copytextfrom.md) - Copy text from a UI element

