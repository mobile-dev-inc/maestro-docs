# Access element text

In order to access text of UI elements, use `copyTextFrom` [command.](https://maestro.mobile.dev/reference/keyboard/copy-and-paste-text) The text can then be accessed via `maestro.copiedText` variable:

```
- copyTextFrom: My Field
- inputText: ${'Hello ' + maestro.copiedText}
```
