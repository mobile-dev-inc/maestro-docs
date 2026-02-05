---
description: Simulate time travel by adjusting the device system clock.
---

# travel

The `travel` command mocks the motion of a user along a specified path at a given speed.

### Parameters

When using the `travel` command, you need to inform the following parameter:

<table><thead><tr><th width="116">Parameter</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>timeout</code></td><td><code>integer</code></td><td>The maximum time to wait, in milliseconds. Defaults to 15000 (15 seconds). If the animation is still running when the timeout is reached, the command succeeds and execution continues. If the animation finishes before the timeout, execution continues immediately.</td></tr></tbody></table>

### Usage examples

This example simulates a user traveling along a route from Paris to Rome at 150 km/s (about 10 seconds).

```yaml
- travel:
    points:
      - "48.8578065, 2.295188"
      - "46.2276, 5.9900"
      - "43.7230, 10.3966"
      - "41.8902, 12.4922"
    speed: 150000
```
