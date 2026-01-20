# Core Selectors

Basic selectors are the most common way to identify elements in Maestro. They allow you to target views using their visible text, accessibility identifiers, or specific screen coordinates.

By default, Maestro uses the accessibility tree to find these elements, ensuring your tests interact with the app just as a user would.

#### Overview

| **Selector** | **Description**                                                     |
| ------------ | ------------------------------------------------------------------- |
| `text`       | Matches the visible text or accessibility label of an element.      |
| `id`         | Matches the accessibility identifier of an element.                 |
| `index`      | Picks a specific occurrence when multiple elements match.           |
| `point`      | Targets a specific coordinate on the screen (Relative or Absolute). |
| `css`        | Web only. Targets elements using standard CSS selectors.            |

{% hint style="info" %}
#### **Regular expressions**

You can handle dynamic values easily because `text` and `id` are regex-based.&#x20;

Remember to escape special characters like `$` or `[` with a double backslash (`\\`).
{% endhint %}

{% hint style="info" %}
#### **Platform specifics**

* **Flutter**: Use Semantics Labels (for `text`) or Accessibility Identifiers (for `id`). Internal Flutter "Keys" are not supported.
* **Android Compose**: Use `Modifier.semantics { testTagsAsResourceId = true }` to ensure your test tags are discoverable as IDs.
{% endhint %}

### `text`

The `text` selector finds elements based on the string displayed on the screen. On Android, this includes `contentDescription`, and on iOS, it includes `accessibilityLabel`.

* **Regex by Default**: All text selectors are treated as regular expressions.
* **Shorthand**: You can skip the key and use a string directly for commands like `tapOn` or `assertVisible`.

```yaml
- tapOn: Login              # Shorthand (matches exactly "Login")
- tapOn: 
    text: ".*Continue.*"      # Regex for partial match
- assertVisible: Submit     # Shorthand for visibility check
```

### `id`

The `id` selector targets the technical identifier of a view. This is highly recommended for dynamic content, icons without text, or localized apps where the visible text changes based on the language.

* **Android**: Maps to the Resource ID.
* **iOS**: Maps to the `accessibilityIdentifier`.

```yaml
- tapOn:
    id: login_button
- assertVisible:
    id: header_icon
```

### `index`

When multiple elements match the same criteria (e.g., three **Add to Cart** buttons on one screen), use `index` to specify which one to interact with. The index is 0-based.

```yaml
# Taps the third instance of an element with the ID "buy_button"
- tapOn:
    id: buy_button
    index: 2
```

### `css`

The `css` selector allows you to target elements in a web application using standard CSS selector syntax. This is particularly useful for targeting classes, IDs, or specific attributes in the DOM. Unlike `text` or `id`, this selector does not support regular expressions.

```yaml
- tapOn:
    css: .secondaryButton
- assertVisible:
    css: "#main-header"
```

### `point`

The `point` selector allows you to interact with specific screen coordinates. This is useful for elements that aren't in the accessibility tree or for tapping specific areas of a large view.

* Relative Position: Defined in percentages (e.g., `"50%, 50%"` for the center).
* Absolute Coordinates: Defined in exact pixels (e.g., `"100, 200"`).

```yaml
- tapOn:
    point: "50%, 50%"   # Taps the dead center of the screen
- tapOn:
    point: "100, 250"   # Taps 100 pixels from left, 250 from top
```
