# pasteText

Paste any text copied with [copyTextFrom](copytextfrom.md) into the currently focused field.\
\
_Note: Make sure your text field is in focus before using this command._

```yaml
- pasteText
```

### Usage Example

Copies text from an element and pastes it into a search field.

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
