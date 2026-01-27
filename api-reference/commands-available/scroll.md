# scroll

The `scroll` command performs a vertical scroll of the current view.

### Syntax

The command takes no arguments.

```yaml
- scroll
```

#### Implementation details

`scroll` is a convenience method that runs an upward swipe from the center of the screen. It is equivalent to:

```yaml
- swipe:
    direction: UP
```

That `swipe` in turn uses `start: 50%, 50%` and `end: 50%, 10%`. The underlying swipe uses a per-platform `duration`: 333 ms on iOS and 400 ms on Android.
