---
description: >-
  Black-box testing for Jetpack Compose via AccessibilityService. Prioritizes
  text-based matching and semantics over testTag for refactoring resilience.
---

# Jetpack

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
