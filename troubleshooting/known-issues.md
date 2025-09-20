# Known Issues

## Cross-platform

### App does not launch

Either the app is not installed or the `appId` is wrong. Note that depending on the app type, the identifier can be different.

To find the appID you can perform the following:

On Android:

1. Execute `adb shell pm list packages` to get a list of all installed packages.
2. Search for the appID manually or use `grep` in the above command to search for part of the name: `adb shell pm list packages | grep <name>`

On iOS

1. Execute `xcrun simctl listapps booted | grep CFBundleIdentifier` to get a list of all installed packages
2. Search for the appID manually or use `grep` in the above command to search for part of the name: `xcrun simctl listapps booted | grep CFBundleIdentifier | grep <name>`&#x20;

### Maestro isn't compatible with all versions of Java

Where the Java version is very old or very new, Maestro might not be immediately compatible. Yeah, we know - switching Java versions is a pain, even moreso if you've got a specific version installed for something else with specific compatibility needs. Use jenv or sdkman to get around this. There's a Maestro guide on how to install and use sdkman [here](https://www.youtube.com/watch?v=yR7BGMjK0vM).

## Android

### Text input is not supported for unicode

Unfortunately, Maestro does not yet have Android support of `inputText` commands that have unicode characters in them (follow [this GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for status updates). Only ASCII characters are supported

### Accidental double tap

Sometimes, tapOn will try to tap again if it doesn't detect a hierarchy change. To fix such cases, use `retryTapIfNoChange`. For example:

```
- tapOn:
    text: "Some Button"
    retryTapIfNoChange: false
```

### Unable to clear state

When running tests against a real device you may receive an error of `(Unable to clear state for app <package>)` when running either:

```yaml
- clearState
```

or:

```yaml
- launchApp:
    clearState: true
```

This error is common on physical devices by Oppo. The workaround is to return to the Developer Settings where ADB Debugging was enabled, and disable 'Verify apps over USB'. Some users have reported needing to enable "Disable permission monitoring" too.

### WebView elements can't be seen by Maestro

Occasionally, web technology renders a page that present a challenge to the OS-native accessibility APIs that Maestro uses. In these cases, you can add `androidWebViewHierarchy: devtools` to the top of your flow so that Maestro can get help from Chrome's DevTools to understand what's on the screen.

```yaml
appId: com.example
androidWebViewHierarchy: devtools
---
- tapOn: Open WebView
- assertVisible: My button
```

Note: support for this in Maestro Studio Desktop is still to come!

## iOS

### `hideKeyboard` command is flaky

On iOS, `hideKeyboard` is done with the help of scrolling up and down from the middle of the screen since there is no native API to hide the keyboard.

If using this command doesn't hide the keyboard we recommend clicking on some non-tappable region with `tapOn` points command, similar to how a user would hide the keyboard when interacting with your app.

### Issues with lists (UICollectionView, UITableView) that fetch data on scroll

Apps that have pagination (fetch data on scroll) inside UITableView / UICollectionView views sometimes result in fetching data at the moments when it is not expected, hanging inside the lists, and flows being broken when testing with Maestro.

There is a bug in XCTest framework that makes UITableView / UICollectionView `willDisplayCell` method being called whenever UI test APIs are being called. Since Maestro relies on XCTest APIs under the hood it might break the pagination logic for some apps.

#### Suggested workaround

Inside `willDisplayCell` check whether the indexPath is really visible via `UITableView.indexPathsForVisibleRows` or `UICollectionView.indexPathsForVisibleItems`:

```swift
// This function should be implemented in a class conforming to UITableViewDelegate
// in case of UICollectionView `collectionView(_:willDisplay:forItemAt:)` from
// UICollectionViewDelegate should be used
func tableView(_ tableView: UITableView,
                   willDisplay cell: UITableViewCell,
                   forRowAt indexPath: IndexPath) {
  // additional check whether the cell is currently visible or not is needed
  // to make sure calls caused by XCTest or other random tableView reloads
  // do not unintentional data fetch request
  guard let visibleIndexPaths = tableView.indexPathsForVisibleRows,
            visibleIndexPaths.contains(indexPath),
            <additional checks that were previosly there> else { return }
        
  print("load new data..")
}
```
