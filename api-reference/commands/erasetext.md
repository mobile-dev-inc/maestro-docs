# eraseText

The  `eraseText` command removes characters from the currently selected text field (if any) and can be used as such:

```yaml
- eraseText # Removes up to 50 characters (default)
```

If you need to remove more characters, you can specify a number explicitly:

```yaml
- eraseText: 100    # Removes up to 100 characters
```

_Note: This is for searches looking for clearText._
