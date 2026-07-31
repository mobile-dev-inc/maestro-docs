---
description: Swipe gestures in any direction with customizable speed and distance.
---

# swipe

The `swipe` command simulates a swipe gesture on the device screen. You can define a swipe by direction, by coordinates, or by starting from a specific UI element.

### Parameters

Depending on the swipe behavior you expected, you need to choose between the following available parameters.

| Parameter               | Description                                                                                                                                                                                                                                                                                                                                                            |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `start`                 | The starting coordinate for the swipe. Specify as `x, y` pixel coordinates or as `x%, y%` percentages relative to the screen dimensions.                                                                                                                                                                                                                              |
| `end`                   | The ending coordinate for the swipe. Specify as `x, y` pixel coordinates or as `x%, y%` percentages relative to the screen dimensions.                                                                                                                                                                                                                                |
| `direction`             | The direction of the swipe. Accepts `LEFT`, `RIGHT`, `UP`, or `DOWN`. This parameter cannot be used with `start` and `end`.                                                                                                                                                                                                                                             |
| `from`                  | An element selector to use as the starting point for the swipe. By default, the swipe begins from the **center** of the matched element. Cannot be used with `start` and `end`. You can add an optional `point` to the element selector to start elsewhere within that element's bounds (same format as [`tapOn` `point`](tapon.md#tap-a-coordinate-within-an-element)). |
| `duration`              | The duration of the swipe in milliseconds. A longer duration results in a slower swipe. Default: `400` milliseconds.                                                                                                                                                                                                                                                  |
| `waitToSettleTimeoutMs` | The maximum time in milliseconds to wait for the screen to settle before executing the next command. This is a best-effort timeout and does not interrupt core operations. Useful for screens with continuous animations like countdown timers.                                                                                                                       |

When using `from`, these nested fields are available on the selector object:

| Nested field | Description                                                                                                                                                                                                               |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `point`      | Optional. A coordinate within the matched element. Use relative percentages (e.g. `"50%, 85%"`) or absolute offsets in pixels within the element (e.g. `"25, 75"`). When omitted, the swipe starts at the element center. |

### Usage examples

The `swipe` command can be configured in several ways to accommodate different testing scenarios.

#### **Swipe by direction**

This example performs a swipe from the right to the left of the screen.

```yaml
- swipe:
    direction: LEFT
```

The `direction` parameter uses the following relative start and end coordinates:

| Direction | Start (width%, height%)       | End (width%, height%)         |
| --------- | ----------------------------- | ----------------------------- |
| `LEFT`    | (90% of width, 50% of height) | (10% of width, 50% of height) |
| `RIGHT`   | (10% of width, 50% of height) | (90% of width, 50% of height) |
| `DOWN`    | (50% of width, 20% of height) | (50% of width, 90% of height) |
| `UP`      | (50% of width, 50% of height) | (50% of width, 10% of height) |

#### **Swipe from an element**

The swipe uses the same end points as a directional swipe in the chosen direction: by default the start is the **center** of the element, and the end follows that direction (e.g. for LEFT, 10% of screen width at the same vertical position).

This example initiates a swipe that starts from the center of the element with the ID `feeditem_identifier` and moves up.

```yaml
- swipe:
    from:
      id: "feeditem_identifier"
    direction: UP
```

#### Swipe from a point within an element

Include a `point` in the `from` selector so that the gesture starts at the designated point within the matched element's bounds instead of its center. This is similar to [tapping a coordinate within an element](tapon.md#tap-a-coordinate-within-an-element).

Some examples of where this might be useful:

- a composite UI e.g a card with an inner image carousel on top and text below, where swiping top/bottom might have different effects
- a swipe-to-unlock control, where swipe needs to be from the left side to the right side of the control to activate

```yaml
- swipe:
    from:
      text: "Desired card text"
      point: "50%, 85%"
    direction: LEFT
```

Percentage values are relative to the **matched element's** width and height (not the screen). Absolute values are pixel offsets from the element's top-left corner.

{% hint style="info" %}
Prefer element selectors with an optional `point` over screen-absolute `start` / `end` coordinates. Absolute screen coordinates make tests brittle across devices and resolutions.
{% endhint %}

#### Swipe by relative coordinates

This example performs a horizontal swipe from the right edge to the left edge of the screen using percentages. This approach ensures the gesture is consistent across devices with different screen dimensions.

```yaml
- swipe:
    start: 90%, 50%
    end: 10%, 50%
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

This example performs a slow swipe by using a duration of 2000 milliseconds.

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
