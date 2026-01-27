# extendedWaitUntil

The `extendedWaitUntil` command pauses the test flow until a specified element becomes visible or not visible on the screen. The command completes as soon as the condition is met. If the condition is not met before the timeout expires, the command fails.

{% hint style="success" %}
Use `extendedWaitUntil` before `assertVisible` or `assertNotVisible` when your app needs longer than the default 7-second timeout. The command keeps checking until the condition is met or your extended timeout is reached, so it does not stop after 7 seconds.
{% endhint %}

### Arguments

<table><thead><tr><th width="118">Argument</th><th>Description</th></tr></thead><tbody><tr><td><code>visible</code></td><td>The selector for the element to wait for. The command proceeds when the element is visible.</td></tr><tr><td><code>notVisible</code></td><td>The selector for the element to wait for. The command proceeds when the element is no longer visible.</td></tr><tr><td><code>timeout</code></td><td>The maximum time to wait, in milliseconds.</td></tr></tbody></table>

For a complete list of available selectors, see the [Selectors](../selectors/) reference.

### Usage examples

#### Wait for an element to be visible

This example waits up to 10 seconds for an element containing the text "My text that should be visible" to appear.

```yaml
- extendedWaitUntil:
    visible: "My text that should be visible"
    timeout: 10000
```

#### Wait for an element to be not visible

This example waits up to 10 seconds for an element with the ID `elementId` to disappear.

```yaml
- extendedWaitUntil:
    notVisible: 
        id: "elementId"
    timeout: 10000
```

### Related content

Learn [how to use wait commands](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/wait-commands) in Maestro to create reliable tests.
