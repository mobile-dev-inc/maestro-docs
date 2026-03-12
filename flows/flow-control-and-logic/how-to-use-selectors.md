---
description: Learn to identify UI elements using text, ID, position, and state selectors.
---

# How to use Selectors

Selectors are the foundational logic Maestro uses to identify UI elements. By default, Maestro interacts with the Accessibility Tree, meaning it sees the application much like an end-user or an assistive device would.&#x20;

### Interaction guide

Most Maestro commands, such as `tapOn`, `assertVisible`, `copyTextFrom`, and `scrollUntilVisible`, require a selector to know which part of the screen to act upon. You can define these selectors using two distinct formats.

When you only need to match an element by its visible text, you can use a simple string. This is the fastest way to write readable tests for static content.

```yaml
- tapOn: Login # Maestro automatically interprets this as { text: "Login" }
```

For higher precision, you can combine multiple attributes into a single Selector block. Maestro will only match an element that satisfies all the provided conditions (an **AND** logic). This is essential when dealing with dynamic UIs, multiple similar buttons, or elements that change state.

```yaml
- tapOn:
    id: submit_button     # Technical ID
    enabled: true         # Only if it's clickable
    below: Password       # Located in a specific area
```

### Best practices

To ensure your test suite remains maintainable and flake-free as your app evolves, follow these strategic principles:

* **Prioritize User-Visible Text**: Whenever possible, use `text` selectors. This ensures your tests validate what the user actually sees and improves test readability by making selectors self-documenting. If the text changes and breaks the test, it usually means the user experience has changed as well.
* **Use IDs for Stability**: For icons, images, or apps supporting multiple languages (localization), use `id` (Accessibility Identifiers). These are hidden from the user but remain constant across different languages.
* **Anchor with Relational Logic**: If an element is dynamic or lacks a unique ID, find a stable "anchor" (like a section header) and use relational selectors (e.g., `below: "Personal Information"`) to pinpoint the target.
* **Handle Dynamic Values with Regex**: Since `text` and `id` are regex-based by default, use patterns like `.*` to handle strings that varies.
* **Verify State Before Action**: When tapping a button that depends on an API call or form validation, include `enabled: true` in your selector. Maestro will automatically wait for the button to become interactive before attempting the tap.

### Selector reference

Explore these specialized reference pages to find the right tool for every UI scenario:

| Category                                                                                              | Best for                                                                               |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| [Core Selectors](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors/core-selectors)             | The essentials: `text`, `id`, `index`, `point`, and `css` (web).                       |
| [Relational Selectors](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors/relational-selectors) | Finding elements based on visual position (`above`, `below`) or structure (`childOf`). |
| [Element Traits](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors/element-traits)             | Filtering by physical characteristics like `square` or `long-text`.                    |
| [State Selectors](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors/state-selectors)           | Verifying functional status (`enabled`, `checked`, `focused`, or `selected`).          |
| [Dimension Matchers](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors/dimension-matchers)     | Targeting by physical size (`width`, `height`) with `tolerance`.                       |

