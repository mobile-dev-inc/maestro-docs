# Wait commands

In a perfect world, apps respond instantly. In reality, network latency, slow animations, and background processing can cause tests to fail because Maestro tries to interact with an element that isn't ready yet.

Maestro provides several ways to handle these timing issues. This guide helps you choose the right strategy to make your Flows resilient and fast.

### Automatic waiting

Before using a dedicated wait command, remember the golden rule of Maestro timing:

> If you expect an element to appear or disappear within a short period (e.g., 5 seconds), use an assertion.

Maestro’s assertions are smart. They don't just check once and fail, they poll the UI continuously until the element appears or the timer expires. This makes them the most efficient way to wait because the test continues immediately after the condition is met.

* [`assertVisible`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/assertvisible): Best for waiting for a screen to load, a success message to appear, or a button to become active.
* [`assertNotVisible`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/assertnotvisible): Best for waiting for a loading spinner to disappear or a modal to close.

```yaml
# assertVisible example
- tapOn: "Submit"
- assertVisible: "Success!" # Maestro will wait for this to appear
```

### Wait strategies

When assertions aren't enough, such as for long-running processes or stabilizing complex animations, you can use one of the specific wait commands.

#### Waiting for long processes (`extendedWaitUntil`)

Use [`extendedWaitUntil`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/extendedwaituntil) for slow network responses (like processing a payment or generating a large report) that are guaranteed to take longer than a few seconds.

This command optimizes your test because Maestro moves on immediately if the element appears faster than the timeout.

```yaml
- extendedWaitUntil:
    visible: "Payment Confirmed"
    timeout: 30000            # Wait up to 30 seconds
```

{% hint style="success" %}
#### **Set realistic timeouts**

Avoid setting every timeout to 60 seconds. If a screen should load in 5 seconds, let the default assertion handle it. This helps catch performance regressions early.
{% endhint %}

#### Waiting for UI stability (`waitForAnimationToEnd`)

Sometimes elements are visible but still moving (e.g., a list sliding into place or a side menu opening). Interacting too early can cause missed taps.

Use the [`waitForAnimationToEnd`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/waitforanimationtoend) command to ensure the test continues only after the animation finishes.

```yaml
- waitForAnimationToEnd:
    timeout: 5000 # Wait up to 5s for movement to stop
```

{% hint style="success" %}
#### Ghost taps

If you experience "ghost taps" (tapping a button that exists but isn't yet clickable), combine your wait logic with [`retryTapIfNoChange: true`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/tapon#retry-a-tap-if-the-ui-is-unresponsive) in your `tapOn` command.
{% endhint %}

### Next steps

For full technical details and parameter lists, visit the individual command pages:

* [`assertVisible`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/assertvisible): Your primary tool for standard waits.
* [`assertNotVisible`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/assertnotvisible): For waiting for elements to disappear.
* [`extendedWaitUntil`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/extendedwaituntil): For smart, long-duration waiting.
* [`waitForAnimationToEnd`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/waitforanimationtoend): For stabilization after UI transitions.

Or continue learning about flow control by exploring the [Loops](loops.md) or [Conditions](conditions.md) guides.
