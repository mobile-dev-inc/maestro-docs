# eraseText

The  `eraseText` command removes up to 50 characters from the currently selected text field (if any):

```yaml
- eraseText
```

If you need to remove more characters, you can specify a number explicitly:

```yaml
- eraseText: 100    # Removes up to 100 characters
```

### Input random text

There are several convenience methods for entering a random text input:

```yaml
- inputRandomEmail       # Enters a random Email address
- inputRandomPersonName  # Enters a random person name
- inputRandomNumber      # Enters a random integer number
- inputRandomText        # Enters random unstructured text
```
