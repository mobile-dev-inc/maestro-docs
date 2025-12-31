# SwiftUI support in Maestro

Maestro provides native, transparent support for iOS applications built with **SwiftUI**. Due to its fundamental "arm's length" architecture, Maestro operates on rendered visual output rather than internal view hierarchies, enabling framework-agnostic UI automation.

Maestro interacts with SwiftUI components identically to UIKit, React Native, or Flutter: by simulating authentic user interactions through the accessibility layer and visual recognition.

## Framework-agnostic architecture

When testing SwiftUI applications with Maestro, you eliminate the need for invasive test instrumentation or view hierarchy dependencies.

* **Visual Recognition:** Maestro analyzes rendered screen content via the iOS accessibility layer. If your SwiftUI code renders a button labeled "Submit," Maestro identifies and interacts with it at the UI layer.
* **Black-Box Testing:** Tests operate independent of implementation details. Maestro doesn't differentiate between `List`, `LazyVStack`, or custom `Button` components—it only interacts with the final rendered interface.

## Element selection strategies

Robust SwiftUI element interaction in Maestro relies on visible text and semantic accessibility identifiers.

### Text-based selection
Since SwiftUI is declarative and content-centric, most interactions reference rendered text directly.
* **Command:** `- tapOn: "Submit Order"`
* **Mechanism:** Maestro scans the screen, locates text rendered by SwiftUI, and executes the tap gesture.

### Accessibility identifiers
For text-less elements such as icons and custom controls, or for disambiguating duplicate elements, leverage iOS accessibility metadata.
* **SwiftUI Implementation:** Apply `.accessibilityIdentifier("elementId")` to components.
* **Maestro Integration:** Use **Maestro Studio** to inspect the accessibility tree. Studio reveals exposed identifiers, allowing you to auto-generate YAML commands via point-and-click inspection.

## Scrollable collections

Maestro intelligently manages navigation through SwiftUI collection views such as `List` and `ScrollView`.

* **`scrollUntilVisible` Command:** Eliminates manual scroll coordinate calculation. Maestro automatically scrolls until the target element appears.
    * **Implementation:** Combines visibility assertions with `assertVisible` and swipe actions with `swipe`, iterating until the target locates the element.
    * **Use Case:** Locating dynamically loaded items in infinite-scroll lists built with SwiftUI.

## Refactoring resilience and visual regression testing

A critical advantage of Maestro with SwiftUI is **visual regression guarantee** during incremental UIKit-to-SwiftUI migrations.

* **Scenario:** You rewrite a legacy UIKit login screen entirely in SwiftUI.
* **Result:** If the rendered interface and text remain visually identical from the user's perspective, Maestro tests **require no modification**. Tests pass with `Pass` status, validating that refactoring preserved user experience despite significant code changes.

## Best practices: Maestro Studio workflow

Use **Maestro Studio** when authoring SwiftUI test flows, as SwiftUI's nested view composition can obscure element hierarchy:

1. Inspect the accessibility tree to understand how Maestro resolves elements.
2. Validate commands interactively in the REPL before persisting to YAML, ensuring interactive elements and secure inputs respond correctly.
3. Generate YAML commands automatically via Studio's point-and-click interface to minimize manual authoring.