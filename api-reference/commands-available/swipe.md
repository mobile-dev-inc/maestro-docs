# swipe

The `swipe` command simulates a swipe gesture on the device screen. You can define a swipe by direction, by coordinates, or by starting from a specific UI element.

### Parameters

Depending on the swipe behavior you expected, you need to choose between the following available parameters.

<table><thead><tr><th width="207.5555419921875">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>start</code></td><td>The starting coordinate for the swipe. Specify as <code>x, y</code> pixel coordinates or as <code>x%, y%</code> percentages relative to the screen dimensions.</td></tr><tr><td><code>end</code></td><td>The ending coordinate for the swipe. Specify as <code>x, y</code> pixel coordinates or as <code>x%, y%</code> percentages relative to the screen dimensions.</td></tr><tr><td><code>direction</code></td><td>The direction of the swipe. Accepts <code>LEFT</code>, <code>RIGHT</code>, <code>UP</code>, or <code>DOWN</code>. This parameter cannot be used with <code>start</code> and <code>end</code>.</td></tr><tr><td><code>from</code></td><td>An element selector to use as the starting point for the swipe. The swipe begins from the center of the specified element. Use the <a data-mention href="../selectors/">selectors</a> available to define the element.</td></tr><tr><td><code>duration</code></td><td>The duration of the swipe in milliseconds. A longer duration results in a slower swipe. Default: <code>400</code> milliseconds.</td></tr><tr><td><code>waitToSettleTimeoutMs</code></td><td>The maximum time in milliseconds to wait for the screen to settle before executing the next command. This is a best-effort timeout and does not interrupt core operations. Useful for screens with continuous animations like countdown timers.</td></tr></tbody></table>

### Usage examples

The `swipe` command can be configured in several ways to accommodate different testing scenarios.

#### Swipe by direction

This example performs a swipe from the right to the left of the screen.

```yaml
- swipe:
    direction: LEFT
```

The `direction` parameter uses the following relative start and end coordinates:

<table><thead><tr><th width="100.88888549804688">Direction</th><th width="205.77777099609375">Start (width%, height%)</th><th>End (width%, height%)</th></tr></thead><tbody><tr><td><code>LEFT</code></td><td>(90% of width, 50% of height)</td><td>(10% of width, 50% of height)</td></tr><tr><td><code>RIGHT</code></td><td>(10% of width, 50% of height)</td><td>(90% of width, 50% of height)</td></tr><tr><td><code>DOWN</code></td><td>(50% of width, 20% of height)</td><td>(50% of width, 90% of height)</td></tr><tr><td><code>UP</code></td><td>(50% of width, 50% of height)</td><td>(50% of width, 10% of height)</td></tr></tbody></table>

#### Swipe by relative coordinates

This example performs a horizontal swipe from the right edge to the left edge of the screen using percentages. This approach ensures the gesture is consistent across devices with different screen dimensions.

```yaml
- swipe:
    start: 90%, 50%
    end: 10%, 50%
```

#### Swipe from an element

This example initiates a swipe that starts from the center of the element with the ID `feeditem_identifier` and moves up.

```yaml
- swipe:
    from:
      id: "feeditem_identifier"
    direction: UP
```

#### Swipe by absolute coordinates

This example performs a swipe between two points defined by absolute pixel coordinates.

```yaml
- swipe:
    start: 100, 200
    end: 300, 400
```

{% hint style="warning" %}
Using absolute coordinates is not recommended, as it can cause tests to fail on devices with different screen resolutions.
{% endhint %}

#### Swipe with a custom duration

This example slows down a swipe by setting its duration to 2000 milliseconds.

```yaml
- swipe:
    direction: LEFT
    duration: 2000
```

#### Swipe with a custom settle timeout

This example limits the time Maestro waits for the UI to settle after the swipe to 500 milliseconds.

```yaml
- swipe:
    direction: UP
    waitToSettleTimeoutMs: 500
```
