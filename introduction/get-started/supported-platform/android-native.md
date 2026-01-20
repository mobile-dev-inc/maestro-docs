# Android Native

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Maestro provides a black-box testing approach for native Android applications. By interacting with the app through the Android Accessibility layer rather than internal code instrumentation, you can test production-ready binaries without modifying your source code.

### Technical advantages

* **Zero Instrumentation**: No custom Gradle configurations, `build.gradle` dependencies, or test-specific APK builds are required. You test the exact binary your users receive.
* **Refactoring Resilience**: Migrating from XML-based Views to Jetpack Compose will not break your tests as long as the user-visible text or semantic IDs remain consistent.
* **UI-Layer Interaction**: Maestro interacts with rendered UI elements, ensuring that tests validate the actual user experience rather than internal component states.

### Element interaction strategies

In Android development, there are two ways to build UIs, XML Views (Classic) and Jetpack Compose (Modern). Maestro supports both.

**XML views (standard layouts)**

For traditional View-based layouts, Maestro leverages the `AccessibilityService` to identify and interact with elements via three primary methods:

*   **Text Selection**: Target any view with a `text` property (e.g., `Button`, `TextView`).

    YAML

    ```yaml
    - tapOn: "Login"
    ```
*   **Resource ID**: Access views by their `android:id`. This is ideal for disambiguating identical text elements.

    YAML

    ```yaml
    - tapOn:
        id: "login_button"
    ```
*   **Content Description**: The `android:contentDescription` attribute is surfaced as a text property, making it the "gold standard" for automating icons and image-based buttons.

    YAML

    ```yaml
    - tapOn: "Settings Icon"
    ```

**Jetpack Compose**

Maestro supports Jetpack Compose by traversing the semantic tree. While Compose is declarative, Maestro maps its output to the standard accessibility framework.

* **Text Composables**: Target `Text` elements directly by their displayed string content.
* **Semantics and TestTags**: For elements without text (like FABs or custom graphics), use the `semantics` modifier. By enabling `testTagsAsResourceId`, you can target these using the `id` selector.

You can add a  `testTag` to tell Compose to treat it like a standard Android ID:

```kotlin
Button(
    modifier = Modifier.semantics { 
        // This line makes the tag visible to Maestro's ID selector
        testTagsAsResourceId = true 
    }.testTag("submit_btn")
) { 
    Text("Confirm Order") 
}
```

The tester can target that button by its ID, making the test much more reliable than searching for the text "Confirm Order", which might change or be translated:

```yaml
# In your Maestro Flow
- tapOn:
    id: "submit_btn"
```

#### Handling lists and dynamic content

Native Android often uses `RecyclerView` or `LazyColumn` for long lists. Maestro abstracts the complexity of view recycling through intelligent scrolling.

For example, to scroll to a specific item, instead of calculating scroll offsets, use the built-in intelligence of Maestro to find elements that are currently off-screen.

```yaml
- scrollUntilVisible:
    element:
        text: "Item #50"
    direction: DOWN
```

Maestro will automatically swipe down, wait for the next items to load, and stop only when "Item #50" is detected in the view hierarchy.

### Known limitations

While Maestro can detect and tap on views containing Unicode characters, direct inputting (typing) of Unicode text via the `inputText` command is currently limited on some Android versions.

### Next steps

If you don't know how to create tests with Maestro, access the [Quickstart](../quickstart.md) guide to get up and running in minutes.

To learn how to create tests, refer to the [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) documentation. If you want to explore Maestro solutions, consult the appropriate documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)
