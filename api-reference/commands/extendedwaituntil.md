# extendedWaitUntil

Waits until an element becomes visible. Fails if the element is not visible after the timeout expires. This command will complete as soon as element becomes visible and is not going to wait for timeout to expire.

```yaml
- extendedWaitUntil:
    visible: Element    # Same input as in assertVisible or tapOn
    timeout: 10000      # Timeout in milliseconds
```

Similarly, it can wait until an element disappears:

```yaml
- extendedWaitUntil:
    notVisible: Element
    timeout: 10000
```
