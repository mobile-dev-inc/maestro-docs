# Wait

{% hint style="warning" %}
By design, Maestro highly discourages a pattern of introducing artificial wait blocks as we believe that Maestro is already handling that reasonably well. Commands listed below should be used as a last resort in exceptional cases where a longer wait period is required (i.e. waiting for a video to finish)
{% endhint %}

If you need to wait for an element to become visible _within a reasonable time_ (i.e. 5-10 seconds), use assertions instead.

{% content-ref url="../reference/assertions.md" %}
[assertions.md](../reference/assertions.md)
{% endcontent-ref %}

### extendedWaitUntil

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

### waitForAnimationToEnd

Waits until an ongoing animation/video is fully finished and screen becomes static.

```yaml
- waitForAnimationToEnd
```

Can have an optional timeout (in milliseconds) after which the command is marked as successful and flow continues.

```yaml
- waitForAnimationToEnd:
    timeout: 5000
```
