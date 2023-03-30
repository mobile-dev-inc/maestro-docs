# waitForAnimationToEnd

Waits until an ongoing animation/video is fully finished and screen becomes static.

```yaml
- waitForAnimationToEnd
```

Can have an optional timeout (in milliseconds) after which the command is marked as successful and flow continues.

```yaml
- waitForAnimationToEnd:
    timeout: 5000
```
