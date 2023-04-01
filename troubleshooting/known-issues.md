# Known Issues

### \[Android] Text input is not supported for unicode

Unfortunately, Maestro does not yet have Android support of `inputText` commands that have unicode characters in them (follow [this GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for status updates). Only ASCII characters are supported

### \[Android] Accidental double tap

Sometimes, tapOn will try to tap again if it doesn't detect a hierarchy change. To fix such cases, use `retryTapIfNoChange`. For example:

```
- tapOn:
    text: "Some Button"
    retryTapIfNoChange: false
```

### App does not launch

Either the app is not installed or the `appId` is wrong. Note that depending on the app type, the identifier can be different.

To find the appID you can perform the following:

On Android:

1. Execute `adb shell pm list packages` to get a list of all installed packages.
2. Search for the appID manually or use `grep` in the above command to search for part of the name: `adb shell pm list packages | grep <name>`

On iOS

1. Execute `xcrun simctl listapps booted | grep CFBundleIdentifier` to get a list of all installed packages
2. Search for the appID manually or use `grep` in the above command to search for part of the name: `xcrun simctl listapps booted | grep CFBundleIdentifier | grep <name>`
