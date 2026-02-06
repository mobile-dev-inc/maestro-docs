---
description: Known limitations and workarounds for Maestro on different platforms.
---

# Known issues

Use this page to quickly find known limitations and their workarounds when debugging Maestro tests. Issues are grouped by cross-platform, Android, and iOS.&#x20;

{% hint style="info" %}
#### Report a new bug

If you find a bug that is not listed on this page, [report it here](bug-report.md).
{% endhint %}

### Cross-platform

<details>

<summary>App does not launch</summary>

#### What is happening

The app does not start. Maestro may report that the app is not installed or that the `appId` is incorrect. The correct identifier depends on the app type.

#### How to find the `appId`

To find the `appId` on Android:

* Run `adb shell pm list packages` to list installed packages.
* Search for the `appId` or filter by name using `adb shell pm list packages | grep <name>`, replacing `<name>` with the desired app name.

On iOS:

* Run `xcrun simctl listapps booted | grep CFBundleIdentifier` to list installed apps.
* Search for the app ID or filter by name using `xcrun simctl listapps booted | grep CFBundleIdentifier | grep <name>`, replacing `<name>` with the desired app name.

</details>

<details>

<summary>Maestro is not compatible with all Java versions</summary>

#### What is happening

Maestro may fail or behave unexpectedly when used with very old or very new Java versions.

#### **Workaround**

We recommend Java 17 or 21. If you require different versions to run other applications, use jenv or sdkman to manage multiple Java versions. See the [Maestro guide on installing and using sdkman](https://www.youtube.com/watch?v=yR7BGMjK0vM).

</details>

### Android

Below are the known issues that affect Maestro when testing Android apps.

<details>

<summary>Text input is not supported for Unicode</summary>

#### What is happening

When testing Android apps, the [`inputText`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/inputtext) command does not work as expected when the input contains non-ASCII characters.

#### **Limitation**

On Android, only ASCII characters are supported. Follow [this GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for updates.

</details>

<details>

<summary>Unable to clear state</summary>

#### What is happening

When testing on a physical Android device, you may see the error `(Unable to clear state for app <package>)` when running:

```yaml
- clearState
```

or

```yaml
- launchApp
   clearState: true
```

#### **Workaround**

This issue is common on some physical devices from Oppo. To resolve it, return to the Developer Settings where ADB debugging was enabled:

1. Open **Developer Settings** (where you enabled ADB debugging).
2. Disable **Verify apps over USB**.
3. If the error persists, enable **Disable permission monitoring**.

</details>

<details>

<summary>WebView elements cannot be seen by Maestro</summary>

#### What is happening

In some cases, web content rendered inside a WebView may not be fully accessible through the OS-native accessibility APIs that Maestro relies on. As a result, Maestro may have difficulty detecting or interacting with elements on the page.

#### **Workaround**

Enable WebView hierarchy inspection via Chrome DevTools. Add `androidWebViewHierarchy: devtools` at the top of your flow file to allow Maestro to use Chrome’s DevTools to better understand and interact with the on-screen web content.

```yaml
androidWebViewHierarchy: devtools
---
- tapOn: "Open WebView"
- assertVisible: "My button"
```

{% hint style="info" %}
Support for `androidWebViewHierarchy` in Maestro Studio Desktop is not yet available
{% endhint %}

</details>

### iOS

Below are the known issues that affect Maestro when testing iOS apps.

<details>

<summary><code>hideKeyboard</code> command is flaky</summary>

#### What is happening

The `hideKeyboard` command does not always dismiss the keyboard.

iOS does not provide a native API to hide the keyboard. Maestro attempts to dismiss it by scrolling from the center of the screen, which is not always reliable.

#### **Workaround**

Use `tapOn` with the `point` parameter to tap on a non-tappable area of the screen (for example, above or beside the keyboard), mimicking how a user would dismiss it.

</details>

<details>

<summary>Lists that fetch data on scroll ( <code>UITableView / UICollectionView</code> )</summary>

#### What is happening

Apps that implement pagination (that is, fetching data as the user scrolls) inside `UITableView` or `UICollectionView` may exhibit unexpected behavior when tested with Maestro. This can include data being fetched at unintended times, lists appearing to hang, or user flows breaking during test execution.

This behavior is caused by a bug in the XCTest framework where the `willDisplayCell` method of `UITableView` / `UICollectionView` is triggered whenever UI test APIs are invoked. Because Maestro relies on XCTest under the hood, these unintended calls can interfere with pagination logic and lead to flaky or incorrect behavior.

#### **Workaround**

In `willDisplayCell`, ensure that data-loading logic runs only when the cell is actually visible. Use `UITableView.indexPathsForVisibleRows` or `UICollectionView.indexPathsForVisibleItems` and verify that the current `indexPath` is included before fetching data:

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

</details>

