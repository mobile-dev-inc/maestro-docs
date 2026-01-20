# copyTextFrom

The `copyTextFrom` command copies text from a UI element and stores it in memory for later use. To access and use the the copied text in your test, you have to use the `maestro.copiedText` variable.

This command requires a [Selector](../selectors/) to identify the target element.

### Usage examples

The following examples demonstrate how to use the copied text.

#### Paste with the `pasteText`  command

This example copies text from an element with the ID `someId` and pastes it into a search field.

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

#### Access with JavaScript

The copied text is also available in JavaScript through the `maestro.copiedText` property. This example copies the text from `someId` and uses the [`inputText`](inputtext.md) command to add the copied text in the search field selected using `tapOn` .

```yaml
appId: com.example.app
---
- launchApp
- copyTextFrom:
    id: "someId"
- tapOn:
    id: "searchFieldId"
- inputText: ${'Pasted using JavaScript: ' + maestro.copiedText}
```

### Related

* [Selectors](../selectors/)
* [`pasteText`](pastetext.md)
