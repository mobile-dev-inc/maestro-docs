---
description: A simple vertical scroll to move down the screen to see the content below
---

# scroll

The `scroll` command performs a vertical scroll of the current view.

### Syntax

The command takes no arguments.

```yaml
- scroll
```

#### How it works

On a mobile device, the the `scroll` command performs an upward [swipe](swipe.md) from the center of the screen to 10% from the top. It is equivalent to a `swipe` with `direction: UP`.

