---
description: >-
  Copy text from UI elements using copyTextFrom and access via
  maestro.copiedText in JavaScript.
---

# Access Element Text in Maestro JavaScript

In order to access text of UI elements, use `copyTextFrom` [command](../../api-reference/commands/copytextfrom.md). The text can then be accessed via `maestro.copiedText` variable:

```
- copyTextFrom: My Field
- inputText: ${'Hello ' + maestro.copiedText}
```
