---
hidden: true
---

# Page

Maestro provides native, transparent support for iOS applications built with UIKit. Operating at the visual interaction layer rather than the implementation layer, Maestro interacts with rendered UI components regardless of underlying class hierarchies such as `UIButton`, `UITableView`, and `UILabel`.

### Technical advantages

* **Zero Instrumentation**: Maestro does not require test libraries, delegates, or ViewController exposure. You test the exact production binaries (.app or .ipa) distributed to your users.
* **Implementation Agnostic**: Because Maestro validates user-facing features rather than internal code, you can refactor UIKit components to SwiftUI without breaking your tests, provided the visual output remains consistent.
* **Black-Box Model**: Maestro adopts an [arm's length](../how-maestro-works.md) approach, simulating authentic user interactions with the rendered UI without needing access to internal source code.

### Element interaction strategies

Maestro interacts with UIKit components by simulating authentic user interactions through the accessibility layer and visual recognition.

#### **Interacting with views by text**

Primary interaction in UIKit is often done via visible UI text. Any view with text content (like a `UIButton` title) can be targeted directly.

```swift
// In your UIKit Swift code
let button = UIButton()
button.setTitle("Submit Order", for: .normal)
```

You can tap this button in your Flow using the visible text:

```yml
- tapOn: "Submit Order"
```

#### **Using accessibility labels and IDs**

For non-textual elements like icons, or for disambiguating duplicate elements, leverage iOS accessibility metadata. Maestro translates these properties into specific selectors:

* `accessibilityLabel`: Maestro translates this to the `text` selector.
* `accessibilityIdentifier`: Maestro translates this to the `id` selector. This is the gold standard for reliable tests.

```swift
// In your UIKit Swift code
let button = UIButton()
button.accessibilityIdentifier = "login_button_id"
```

The corresponding tap command in your Flow would use the `id`:

```yaml
- tapOn:
    id: "login_button_id"
```

{% hint style="info" %}
If an element has both text content and an `accessibilityLabel`, Maestro will prioritize the `accessibilityLabel` as the value for the `text` selector.
{% endhint %}

### Handling lists and complex components

Maestro abstracts away the complexity of coordinate calculations and cell enumeration in `UITableView` and `UICollectionView`.

#### **Intelligent scrolling**

Instead of manual index or offset calculations, use `scrollUntilVisible`. Maestro combines visibility detection with continuous swiping to find elements that are currently off-screen.

```yaml
- scrollUntilVisible:
    element:
        text: "List Item 50"
    direction: DOWN
```

### Known limitations

* **Real Devices**: Full support for local execution is currently optimized for the iOS Simulator. Physical device support requires proper provisioning and WebDriverAgent setup.
* **Unicode Input**: Similar to Android, direct inputting of Unicode text via `inputText` can be limited depending on the environment, though views containing Unicode are detectable.

### Next steps

If you don't know how to create tests with Maestro, access the [Quickstart](../quickstart.md) guide to get up and running in minutes.

To learn how to create tests, refer to the [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) documentation. If you want to explore Maestro solutions, consult the appropriate documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)
