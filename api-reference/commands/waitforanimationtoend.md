# waitForAnimationToEnd

Waits until an ongoing animation/video is fully finished and screen becomes static.

```yaml
- waitForAnimationToEnd
```

Can have an optional timeout (in milliseconds) after which, if the animation is still running, the command is marked as successful and flow continues regardless. This is a maximum value - if Maestro detects animation has ended before the timeout completes, the flow will continue as normal.

```yaml
- waitForAnimationToEnd:
    timeout: 5000
```

If you want to add a fixed delay, see [sleep](./sleep.md).
