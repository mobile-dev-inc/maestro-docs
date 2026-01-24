# eraseText

The `eraseText` command deletes characters from the currently focused text field by simulating backspace key presses. By default, it removes up to 50 characters, making it an efficient way to clear input fields.

### Syntax

You can use the command without arguments to perform a standard clear, or specify a precise number of characters to delete (up to a maximum of 100).

```yaml
# Removes up to 50 characters (Default)
- eraseText 

# Removes a specific number of characters (Up to 100)
- eraseText: 10
```

### Clearing large text blocks

While `eraseText` works well for short inputs, clearing long paragraphs or very large fields by hitting backspace 50 times can be slow. To optimize your Flow, especially on iOS, you can use the following sequence to select and delete everything at once:

```yaml
# 1. Select the entire text block
- longPressOn: "<your_input_id>"
- tapOn: "Select All"

# 2. Perform a single backspace to clear the selection
- eraseText: 1
```

{% hint style="success" %}
When text is already selected (e.g., after **Select All**), using `- eraseText: 1` is faster than the default `- eraseText`, as it only needs to trigger a single backspace to delete the entire highlighted selection.
{% endhint %}
