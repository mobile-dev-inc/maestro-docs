---
description: >-
  Avoid fixed waits; use assertions and extendedWaitUntil in Maestro. Reserve
  waitForAnimationToEnd for specific cases. Aligns with real device testing.
---

# Wait Commands in Maestro for Reliable Tests



{% hint style="warning" %}
By design, Maestro highly discourages a pattern of introducing artificial wait blocks as we believe that Maestro is already handling that reasonably well. Commands listed below should be used as a last resort in exceptional cases where a longer wait period is required (i.e. waiting for a video to finish)
{% endhint %}

If you need to wait for an element to become visible _within a reasonable time_ (i.e. 5-10 seconds), use assertions instead:

{% content-ref url="../api-reference/commands/assertvisible.md" %}
[assertvisible.md](../api-reference/commands/assertvisible.md)
{% endcontent-ref %}

{% content-ref url="../api-reference/commands/assertnotvisible.md" %}
[assertnotvisible.md](../api-reference/commands/assertnotvisible.md)
{% endcontent-ref %}



### extendedWaitUntil

Waits until an element becomes visible. More documentation can be found in the API reference:

{% content-ref url="../api-reference/commands/extendedwaituntil.md" %}
[extendedwaituntil.md](../api-reference/commands/extendedwaituntil.md)
{% endcontent-ref %}

### waitForAnimationToEnd

Waits until an ongoing animation/video is fully finished and screen becomes static. More information can be found in the API reference:

{% content-ref url="../api-reference/commands/waitforanimationtoend.md" %}
[waitforanimationtoend.md](../api-reference/commands/waitforanimationtoend.md)
{% endcontent-ref %}
