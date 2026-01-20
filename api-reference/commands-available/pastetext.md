# pasteText

The `pasteText` command pastes text from the clipboard into the currently focused UI element.

This command requires that a text field is in focus before execution. Text must first be copied to the clipboard using the [`copyTextFrom` ](copytextfrom.md)command.

### Sintax

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
