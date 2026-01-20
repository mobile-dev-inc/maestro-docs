# swipe

To have control over the swipe gesture, you have the following choices:

### Relative Swipe Using Percentages

You can specify start and end coordinates in percentages to make the swipe gesture consistent across different screen dimensions:

```yaml
- swipe:  
    start: 90%, 50% # From (90% of width, 50% of height)
    end: 10%, 50% # To (10% of width, 50% of height)
```

### Swiping Directions

Swiping in RIGHT, LEFT, UP, or DOWN directions:

1. **LEFT**: From the right to the left of the screen.
2. **RIGHT**: From the left to the right of the screen.
3. **UP**: From the middle of the device to the top of the device.
4. **DOWN**: From the top of the device to the bottom of the device.

Example:

```yaml
- swipe:              # This command swipes in the left direction from the middle of the device. 
    direction: LEFT
```

Relative start and end coordinates for directional swipe are configured as follows:

<table><thead><tr><th width="156" align="center">Direction</th><th width="286.3333333333333" align="center">Start (x%, y%)</th><th align="center">End (x%, y%)</th></tr></thead><tbody><tr><td align="center">LEFT</td><td align="center">(90% of width, 50% of height)</td><td align="center">(10% of width, 50% of height)</td></tr><tr><td align="center">RIGHT</td><td align="center">(10% of width, 50% of height)</td><td align="center">(90% of width, 50% of height)</td></tr><tr><td align="center">DOWN </td><td align="center">(50% of width, 20% of height)</td><td align="center">(50% of width, 90% of height)</td></tr><tr><td align="center">UP</td><td align="center">(50% of width, 50% of height)</td><td align="center">(50% of width, 10% of height)</td></tr></tbody></table>

A common use case for this is to swipe the onboarding pages.

### Swiping elements

You can also specify elements as a starting point for swipe commands. It will swipe from the middle of the element in the direction you specify. Example:

```yaml
- swipe:
   from: 
     id: "feeditem_identifier" # From (x, y) center of element
   direction: UP # To (50% of width, 10% of height)
    
```

Note that you can use any selector here to target an element to swipe from. Please refer to the [Selectors](../selectors.md) page for a full list of available selectors.

### Swiping Coordinates

You can also specify start and end points for the swipe to have more control:

```yaml
- swipe:                 # This command swipes from point (x:100, y:200) to point (x: 300, y:400). Units are in pixels
    start: 100, 200
    end: 300, 400
```

{% hint style="warning" %}
It is not recommended to use absolute coordinates when swiping as this might mean that your test won't work on a device with a different screen configuration.
{% endhint %}

### Swiping speed

To control swiping speed you can use duration in the swipe command. The more the duration slower the swipe. By default, the swipe command uses 400 milliseconds. To configure speed you can use:

```yaml
- swipe:
    direction: LEFT
    duration: 2000      # Values are in ms.
```

### Control wait time

Maestro usually waits for the screen to settle before moving to the next command, however that is not always desirable.

If your app or screen has the following:

* Moving elements like a countdown timer
* Non-blocking animations that are part of the UI

Then, you can use `waitToSettleTimeoutMs` to limit the time Maestro waits for things to settle

```yaml
- swipe:
    direction: UP
    waitToSettleTimeoutMs: 500 # ms
```

**Note:** This will be a best effort timeout. Maestro will not interrupt core operations to honor the timeout.
