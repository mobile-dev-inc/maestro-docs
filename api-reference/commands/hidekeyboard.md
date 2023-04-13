# hideKeyboard

### hideKeyboard

To hide the software keyboard, use `hideKeyboard` command:

```yaml
- hideKeyboard
```

#### iOS implementation caveat

On iOS, `hideKeyboard` is done with help of scrolling up and down from the middle of the screen since there is no native API to hide the keyboard. If using this command doesn't hide the keyboard we recommend clicking on some non-tappable region with `tapOn` points command, similarly to how a user would hide the keyboard when interacting with your app.
