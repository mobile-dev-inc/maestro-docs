# copyTextFrom

The `copyTextFrom` command copies text from a UI element and stores it in memory. This command requires a [Selector](../selectors/) to identify the target element.

### Accessing the copied text

When you copy content using the `copyTextFrom` command, you have two ways to use the text after it has been copied:

1. Use the [`pasteText`](pastetext.md) command to immediately insert the content into a focused field.
2. To run an equality check, perform complex logic, or store the text for later use in your flow, use the `maestro.copiedText` variable.

### Usage examples

The following examples demonstrate how to use the copied text.

#### Paste with the `pasteText`  command

This example copies text from an element with the ID `someId` and pastes it into a search field.

```yaml
appId: com.example.app
---
- launchApp
- copyTextFrom:
    id: "someId"
- tapOn:
    id: "searchFieldId"
- pasteText
```

#### Access with JavaScript

The copied text is available in JavaScript through the `maestro.copiedText` property. This example copies the text from `someId` and uses the [`inputText`](inputtext.md) command to add the content into the search field.

```yaml
appId: com.example.app
---
- launchApp
- copyTextFrom:
    id: "someId"
- tapOn:
    id: "searchFieldId"
- inputText: ${'Pasted using JavaScript: ' + maestro.copiedText}
```

#### **Store and validate**

You can assign the copied value to a custom variable to perform assertions or use it later in a Flow after other commands have overwritten the clipboard.&#x20;

This example demonstrates how to copy text from a UI element, store the copied value in a variable using `maestro.copiedText`, and then validate that the captured text matches the expected value.

```yaml
# Copy text from an element
- copyTextFrom:
    id: "my_element"

# Store the value for later use
- evalScript: ${output.myElementText = maestro.copiedText}

# Check that the element had the correct value
- assertTrue: ${output.myElementText == "Correct Text"}
```

### Related content

Explore how the [`pasteText`](pastetext.md) command works, or learn how to use the available [Selectors](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/how-to-use-selectors) to define the desired element when copying content.
