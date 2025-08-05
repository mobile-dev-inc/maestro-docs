---
description: >-
  Copy text from UI elements with copyTextFrom and access it via
  maestro.copiedText in JavaScript scripts.
---

# Access element text

In order to access text of UI elements, use `copyTextFrom` [command](../../api-reference/commands/copytextfrom.md). The text can then be accessed via `maestro.copiedText` variable:

```
- copyTextFrom: My Field
- inputText: ${'Hello ' + maestro.copiedText}
```
