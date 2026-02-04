---
description: Wait for UI animations to complete before proceeding.
---

# waitForAnimationToEnd

The `waitForAnimationToEnd` command pauses command execution until on-screen animations or videos complete and the UI becomes static.

### Parameters

This command accepts the following optional parameter:

<table><thead><tr><th width="122">Parameter</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>timeout</code></td><td><code>integer</code></td><td>The maximum time to wait, in milliseconds. Defaults to 15000 (15 seconds). If the animation is still running when the timeout is reached, the command succeeds and execution continues. If the animation finishes before the timeout, execution continues immediately.</td></tr></tbody></table>

### Usage examples

The following example waits for an animation to finish without a timeout. As a result, the next step is executed only after the animation ends.

```yaml
- waitForAnimationToEnd
```

The following example waits for an animation to finish with a maximum timeout of 5,000 milliseconds. If the animation ends before the timeout, Maestro continues execution without waiting for the full timeout. If the animation does not finish before the timeout is reached, the command is marked as successful, and the flow continues.

```yaml
- waitForAnimationToEnd:
    timeout: 5000
```
