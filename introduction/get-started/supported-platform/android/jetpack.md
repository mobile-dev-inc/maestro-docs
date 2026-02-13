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

### Next steps

If you don't know how to create tests with Maestro, access the [QuickStart](../../quickstart.md) guide to get up and running in minutes.

To learn how to create tests, refer to the [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) documentation. If you want to explore Maestro solutions, consult the appropriate documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)
