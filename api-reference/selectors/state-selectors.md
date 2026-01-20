# State Selectors

State Selectors allow you to filter UI elements based on their current functional or interactive status. These are primarily used to verify that an element is ready for interaction, has been correctly updated by a previous action, or to find a specific element among several identical ones (e.g., finding the selected tab in a navigation bar).

### **Overview**

All state selectors accept a boolean value (`true` or `false`).

| **Selector** | **Description**                                                                            |
| ------------ | ------------------------------------------------------------------------------------------ |
| `enabled`    | Matches elements based on whether they are currently interactive or "grayed out."          |
| `checked`    | Matches elements based on their toggle state (Checkboxes, Radio Buttons, Switches).        |
| `focused`    | Matches the element that currently has keyboard input focus.                               |
| `selected`   | Matches elements currently marked as selected (often used for Tabs or Segmented Controls). |

{% hint style="success" %}
#### Usage tips

State Selectors are most effective when combined with [Core Selectors](https://www.google.com/search?q=core-selectors). For example, finding a specific button that is also enabled: `tapOn: { text: "Next", enabled: true }`.
{% endhint %}

### `enabled`

The `enabled` selector is essential for ensuring that an app’s logic is functioning correctly. For example, a "Submit" button should remain disabled (`enabled: false`) until all required fields are filled.

```yaml
# Assert that the login button is disabled initially
- assertVisible:
    id: login_button
    enabled: false

# Tap the button once it becomes active
- tapOn:
    id: login_button
    enabled: true
```

### `checked`

This selector is specifically for elements that hold a binary state, such as checkboxes, radio buttons, and switches.

```yaml
# Find the checkbox that is currently checked
- assertVisible:
    id: "remember_me_checkbox"
    checked: true

# Ensure a switch is turned off
- assertVisible:
    id: notifications_switch
    checked: false
```

### `focused`

The `focused` selector identifies the element that is currently active for text input. This is useful for verifying that `tapOn` correctly placed the cursor in the right field or that an app automatically focuses the first input field on a form.

```yaml
# Verify that the 'Search' input field has focus
- assertVisible:
    id: search_input
    focused: true
```

### `selected`

While similar to `checked`, `selected` is typically used for navigation elements like tabs, segmented controls, or specific items in a list that have been highlighted.

```yaml
# Find the 'Profile' tab only if it is the currently selected one
- tapOn:
    text: Profile
    selected: true
```

