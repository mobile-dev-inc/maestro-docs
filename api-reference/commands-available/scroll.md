---
description: Scroll the screen up, down, left, or right by a specified amount.
---

# scroll

The `scroll` command performs a vertical scroll of the current view.

### Syntax

The command takes no arguments.

```yaml
- scroll
```

#### How it works

`scroll` runs an upward swipe from the center of the screen (`start: 50%, 50%`; `end: 50%, 10%`). It is equivalent to `swipe: direction: UP`. The swipe uses a per-platform duration: 333 ms on iOS and 400 ms on Android.
