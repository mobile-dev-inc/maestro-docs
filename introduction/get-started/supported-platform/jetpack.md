---
description: >-
  Black-box testing for Jetpack Compose via AccessibilityService. Prioritizes
  text-based matching and semantics over testTag for refactoring resilience.
---

# Jetpack

Maestro follows a fundamental principle: **UI-level automation without framework intrusion**. Unlike instrumentation-based tools such as Espresso or Robolectric, which execute inside the app process and depend on framework-specific APIs, Maestro operates externally using Android’s system automation interfaces. This allows Maestro to perform reliable black-box testing regardless of whether your UI is implemented with XML Views, Jetpack Compose, or other UI frameworks.

### Architecture-agnostic testing philosophy

Maestro interacts with your application the same way the Android system and users do, using accessibility metadata and system-level automation. This provides several key advantages:

* **Framework independence:** Maestro does not depend on Compose internals such as composition state, recomposition cycles, or render tree structure. Tests remain valid regardless of UI implementation details.
* **System-level element discovery:** Maestro locates elements using accessibility metadata, visible text, resource identifiers, and other stable attributes exposed by the Android system. This ensures compatibility with Compose, XML Views, and hybrid applications.
* **Stable selector model:** Element identification relies on externally observable properties such as visible text, accessibility labels (`contentDescription`), and resource IDs, rather than internal framework constructs.

### Refactoring resilience

Maestro tests are designed to validate user workflows rather than internal implementation details. This provides strong resilience during UI refactoring, including migration from XML-based layouts to Jetpack Compose.

* **Semantic stability:** As long as visible text, accessibility metadata, or resource identifiers remain consistent, existing Maestro tests typically continue to work without modification.
* **Implementation independence:** Tests verify behavior from the user’s perspective, protecting against failures caused by internal architectural changes that do not affect the user experience.

### Element interaction patterns

Maestro interacts with UI elements using selectors based on system-exposed properties rather than framework-specific APIs.

#### Element selection strategy

Maestro supports multiple stable selector types, including:

*   **Visible text**

    ```yaml
    - tapOn: "Login"
    ```

    Matches elements displaying the specified text.
*   **Accessibility labels**

    Elements with accessibility metadata such as:

    ```kotlin
    Modifier.semantics {
        contentDescription = "Login Button"
    }
    ```

    can be targeted directly:

    ```yaml
    - tapOn:
        description: "Login Button"
    ```
*   **Resource identifiers**

    When available, resource IDs provide highly stable selectors:

    ```yaml
    - tapOn:
        id: "login_button"
    ```

These selector strategies work consistently across Compose and View-based interfaces.

### Compatibility with Jetpack Compose semantics

Jetpack Compose exposes accessibility metadata through its semantics system. Maestro automatically uses this information when available, including:

* Visible text from composables such as `Text` and `Button`
* Accessibility descriptions defined with `contentDescription`
* Resource identifiers when provided

This enables reliable interaction without requiring Compose-specific test APIs or instrumentation.

### Comparative advantages

| Aspect                     | Maestro                             | Instrumentation Tools  |
| -------------------------- | ----------------------------------- | ---------------------- |
| Execution model            | External (black-box)                | In-process (white-box) |
| Framework dependency       | None                                | High                   |
| Compose internals required | No                                  | Yes                    |
| Test infrastructure in app | Not required                        | Required               |
| Refactoring resilience     | High (when semantics remain stable) | Moderate to low        |
| Accessibility usage        | Recommended for reliability         | Optional               |

Maestro eliminates the need for app-side test infrastructure code, lowering barriers for QA practitioners lacking native Android development expertise.





















Maestro operates on a fundamental principle: **UI-level automation without framework intrusion**. Unlike instrumentation-based tools (for example, Espresso, Robolectric) that execute within the app process and require deep coupling to view hierarchies, Maestro performs black-box testing through accessibility layer integration and visual element detection.

## Architecture-agnostic testing philosophy

The archtecture-agnóstic approach of Maestro have some several technical advantages:

* **Framework Decoupling:** Maestro's test harness remains independent of Compose's internal state management, composition recomposition cycles, or render tree structure.
* **Accessibility Tree Traversal:** Maestro queries the Android AccessibilityService to locate interactive elements, ensuring compatibility regardless of whether the UI layer uses XML layouts, Jetpack Compose, Flutter, or other declarative frameworks.
* **Visual Semantics:** Element identification prioritizes semantic metadata (`contentDescription`, visible text) over implementation-specific identifiers (`testTag`, `resourceId`).

## Refactoring resilience

Migrating from View-based (XML) to Compose-based UI reduces test maintenance overhead significantly:

* **Semantic Stability:** If UI semantics remain consistent after refactoring, Maestro test specifications require no modifications, eliminating brittleness introduced by implementation-level changes.
* **Behavior-Driven Validation:** Tests verify user workflows rather than internal component state, providing protection against architectural changes that preserve UX.

## Element interaction patterns

The Maestro tests interacts witht the UI of your application according to the following patterns:

### Element selection strategy

Maestro leverages stable, user-visible identifiers over Compose-specific constructs:

* **Text-Based Matching:** `tapOn: "Login"` targets elements by visible string content, reducing dependency on volatile `testTag` assignments.
* **Accessibility Labels:** Components with `semantics { contentDescription = ... }` are automatically discoverable without additional test configuration.

### Standard command set

Maestro applies uniform command semantics across all UI frameworks:

* `tapOn`: Touch gesture on identified elements.
* `inputText`: Text input into `TextField` composables.
* `scrollUntilVisible`: Lazy composition traversal. Particularly effective for `LazyColumn`/`LazyRow` where incremental rendering requires dynamic scroll-to-find behavior.

## Comparative advantages

| Aspect                    | Maestro              | Instrumentation Tools  |
| ------------------------- | -------------------- | ---------------------- |
| Process Context           | External (black-box) | In-process (white-box) |
| Framework Dependency      | None                 | High coupling          |
| Refactoring Impact        | Minimal              | Significant            |
| Accessibility Requirement | Yes (benefits)       | Optional               |

Maestro eliminates the need for app-side test infrastructure code, lowering barriers for QA practitioners lacking native Android development expertise.
