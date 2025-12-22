# Reference: UIKit support in Maestro

Maestro provides native, transparent support for iOS apps built with UIKit. Operating at the visual interaction layer rather than the implementation layer, Maestro interacts with rendered UI components regardless of underlying class hierarchies such as `UIButton`, `UITableView`, and `UILabel`.

## Black box testing model
Maestro adopts an "extreme arm's length" approach, simulating user interactions with the rendered UI without instrumenting app code or accessing internal implementation details.

*   **Zero Instrumentation:** No test libraries, delegates, or viewController exposure required. Maestro tests production binaries such as `.app` and `.ipa` files as distributed to end users.
*   **Implementation Agnostic:** Refactoring UIKit to SwiftUI without visual/textual changes preserves test validity. Maestro validates user-facing features, not implementation.

## Text-based selection
Primary interaction method via visible UI text:

```yaml
- tapOn: "Save"
```

## Accessibility layer
For non-textual elements such as icons and image buttons, or for disambiguation:
*   Define `accessibilityIdentifier` on UIView instances
*   Maestro Studio auto-inspects and reveals IDs for command generation

## Collection views: UITableView and UICollectionView
Maestro abstracts cell enumeration and coordinate calculation through intelligent scrolling:

```yaml
- scrollUntilVisible:
    element:
        text: "List Item 50"
    direction: DOWN
```

This command combines visibility detection with continuous swiping, eliminating manual index/offset calculations.

## Supported Gestures

*   **Tap:** Single touch interactions
*   **Text Input:** UITextField/UITextView population with optional credential injection
*   **Swipe:** ViewController transitions and carousel navigation

## Advantages Over XCUITest
Unlike XCUITest's fragility and complex element queries, Maestro reduces technical friction by operating solely on rendered output, enabling QA and non-expert developers to author robust tests.
