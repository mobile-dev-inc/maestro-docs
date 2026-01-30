# Known issues

Use this page to quickly find known limitations and their workarounds when debugging Maestro tests. Issues are grouped by **cross-platform**, **Android**, and **iOS**. To report something not listed here, see Bug report.

### Cross-platform

#### App does not launch

**What you see:** The app does not start; Maestro may report that the app is not installed or the `appId` is wrong. The correct identifier depends on the app type.

**How to find the app ID**

{% tabs %}
{% tab title="Android" %}
1. Run `adb shell pm list packages` to list installed packages.
2. Search for the app ID or filter by name: `adb shell pm list packages | grep <name>`
{% endtab %}

{% tab title="iOS" %}
1. Run `xcrun simctl listapps booted | grep CFBundleIdentifier` to list installed apps.
2. Search for the app ID or filter by name: `xcrun simctl listapps booted | grep CFBundleIdentifier | grep <name>`
{% endtab %}
{% endtabs %}

#### Maestro is not compatible with all Java versions

**What you see:** Maestro may fail or behave unexpectedly with very old or very new Java versions.

**What to do:** Use **jenv** or **sdkman** to manage multiple Java versions. See the [Maestro guide on installing and using sdkman](https://www.youtube.com/watch?v=yR7BGMjK0vM).

### Android

Issues that affect Maestro when testing Android apps.

<details>

<summary>Text input is not supported for Unicode</summary>

**What you see:** `inputText` does not work as expected when the text contains non-ASCII characters.

**Limitation:** On Android, only ASCII characters are supported. Follow [this GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for updates.

</details>

<details>

<summary>Accidental double-tap</summary>

**What you see:** `tapOn` sometimes triggers a second tap when the UI hierarchy does not change after the first tap.

**Workaround:** Disable retry by setting `retryTapIfNoChange: false`:

```yaml
- tapOn:
    text: "Some Button"
    retryTapIfNoChange: false
```

</details>

<details>

<summary>Unable to clear state</summary>

**What you see:** On a real device, you get `(Unable to clear state for app <package>)` when using `clearState` or `launchApp` with `clearState: true`.

**Workaround:** This is common on some physical devices (for example, Oppo).

1. Open **Developer Settings** (where you enabled ADB debugging).
2. Disable **Verify apps over USB**.
3. If the error persists, enable **Disable permission monitoring**.

</details>

<details>

<summary>WebView elements cannot be seen by Maestro</summary>

**What you see:** Maestro does not find elements inside a WebView; assertions or taps on web content fail.

**Workaround:** Add `androidWebViewHierarchy: devtools` at the top of your flow so Maestro can use Chrome DevTools to understand the WebView:

```yaml
appId: com.example
androidWebViewHierarchy: devtools
---
- tapOn: "Open WebView"
- assertVisible: "My button"
```

{% hint style="info" %}
Support for \`androidWebViewHierarchy: devtools\` in Maestro Studio Desktop is still to come.
{% endhint %}

</details>

***

### iOS

Issues that affect Maestro when testing iOS apps.

<details>

<summary><code>hideKeyboard</code> command is flaky</summary>

**What you see:** The `hideKeyboard` command does not always dismiss the keyboard.

**Why:** iOS has no native API to hide the keyboard. Maestro tries to dismiss it by scrolling from the center of the screen, which is not always reliable.

**Workaround:** Use `tapOn` with the `point` parameter on a non-tappable area of the screen (for example, above or beside the keyboard), the same way a user would tap to dismiss it.

</details>

<details>

<summary>Lists that fetch data on scroll ( <code>UITableView / UICollectionView</code> )</summary>

**What you see:** Lists with pagination load data at the wrong time, hang, or break the flow when tested with Maestro.

**Why:** A bug in XCTest causes `willDisplayCell` to be called when UI test APIs are used. Maestro uses XCTest, so it can trigger this and break your pagination logic.

**Workaround:** In `willDisplayCell`, only run your load logic when the cell is actually visible. Use `UITableView.indexPathsForVisibleRows` or `UICollectionView.indexPathsForVisibleItems` and confirm the current `indexPath` is in that set before fetching:

```swift
// Implement in a class conforming to UITableViewDelegate.
// For UICollectionView, use collectionView(_:willDisplay:forItemAt:) from UICollectionViewDelegate.
func tableView(_ tableView: UITableView,
               willDisplay cell: UITableViewCell,
               forRowAt indexPath: IndexPath) {
  guard let visibleIndexPaths = tableView.indexPathsForVisibleRows,
        visibleIndexPaths.contains(indexPath) else { return }
  // Add your existing visibility or load conditions here, then fetch data.
  print("load new data..")
}
```

</details>

***

### Related Content

* FAQ: Common questions and answers.
* Bug report: How to report a new issue.
