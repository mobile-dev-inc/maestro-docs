# Known Issues

### \[Android] Text input is not supported for unicode

Unfortunately, Maestro does not yet have Android support of `inputText` commands that have unicode characters in them (follow [this GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for status updates). Only ASCII characters are supported

### \[Android] Accidental double tap

Sometimes, tapOn will try to tap again if it doesn't detect a hierarchy change. To fix such cases, use `retryTapIfNoChange.`  For example:

```
- tapOn:
    text: "Some Button"
    retryTapIfNoChange: false
```
