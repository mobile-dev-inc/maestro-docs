# pasteText

Paste any text copied with [copyTextFrom](copytextfrom.md) into the currently
focused field.

{% hint style="info" %}
Make sure your text field is in focus before using this command.
{% endhint %}

```yaml
- pasteText
```

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
