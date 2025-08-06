---
description: >-
  Copy text from elements and store in maestro.copiedText for reuse in tests or
  scripts.
---

# copyTextFrom

You can copy text from an element and save it in-memory, to paste later. To find the element you wish to copy text from you can use Selectors. For a full list of what selectors are available, please refer to the [Selectors](../selectors.md) page.

### Usage Example

Copy text from an element and paste it into a search field:

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

The copied text can also be access in JavaScript using the `maestro.copiedText` property:

```
appId: com.example.app
---
- launchApp
- copyTextFrom:
    id: "someId"
- tapOn:
    id: "searchFieldId"
- inputText: ${'Pasted using JavaScript: ' + maestro.copiedText}
```
