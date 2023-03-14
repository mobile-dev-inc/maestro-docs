# Scroll and Swipe

To do a simple vertical scroll you can simply say:

```yaml
- scroll
```

### Swiping

To have control over the swipe gesture, you have the following choices:

#### **Relative Swipe Using Percentages**

You can specify start and end coordinates in percentages to make the swipe gesture consistent across different screen dimensions:

```yaml
- swipe:  
    start: 90%, 50% # From (90% of width, 50% of height)
    end: 10%, 50% # To (10% of width, 50% of height)
```

#### **Swiping Directions**&#x20;

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

| Direction |         Start (x%, y%)        |          End (x%, y%)         |
| :-------: | :---------------------------: | :---------------------------: |
|    LEFT   | (90% of width, 50% of height) | (10% of width, 50% of height) |
|   RIGHT   | (10% of width, 50% of height) | (90% of width, 50% of height) |
|   DOWN    | (50% of width, 20% of height) | (50% of width, 90% of height) |
|     UP    | (50% of width, 50% of height) | (50% of width, 10% of height) |

A common use case for this is to swipe the onboarding pages.

#### **Swiping elements**

You can also specify elements as a starting point for swipe commands. It will swipe from the middle of the element in the direction you specify. Example:

```yaml
- swipe:
   from: 
     id: "feeditem_identifier" # From (x, y) center of element 
   direction: UP # To (50% of width, 10% of height)
    
```

#### **Swiping Coordinates**

You can also specify start and end points for the swipe to have more control:

```yaml
- swipe:                 # This command swipes from point (x:100, y:200) to point (x: 300, y:400). Units are in pixels
    start: 100, 200
    end: 300, 400
```

{% hint style="warning" %}
It is not recommended to use absolute coordinates when swiping as this might mean that your test won't work on a device with a different screen configuration.
{% endhint %}

#### Swiping speed

To control swiping speed you can use duration in the swipe command. The more the duration slower the swipe. By default, the swipe command uses 400 milliseconds. To configure speed you can use:

```yaml
- swipe:
    direction: LEFT
    duration: 2000      # Values are in ms.
```

###

### ScrollUntilVisible

To scroll towards a direction until an element becomes visible in the view hierarchy, use the following command:

<pre class="language-yaml"><code class="lang-yaml"><strong>- scrollUntilVisible:
</strong>    element:
      id: "viewId" # (optional) Finds view with id that matches regexp
      text: "MyElementText" # (optional) Finds view with text that matches regexp
    direction: DOWN # DOWN|UP|LEFT|RIGHT (optional, default: DOWN)
    timeout: 50000 # (optional, default: 20000ms)
    speed: 40 # 0-100 (optional, default: 40) Scroll speed. Higher values scroll faster.
    visibilityPercentage: 100 # 0-100 (optional, default 100) Percentage of element visible in viewport
</code></pre>

#### Direction

The scroll will move towards the direction specified `DOWN|UP|LEFT|RIGHT`. For example, if `DOWN` is specified then it will start scrolling towards the bottom of the screen.

#### Visibility Percentage

By default an element will be considered visible if it is fully displayed in the viewport. You can adjust that threshold by modifying `visibilityPercentage`.

#### Example

If we want to scroll towards the bottom until a view with id `com.example.resource.some_view_id` becomes visible:

```yaml
- scrollUntilVisible:
    element:
      id: ".*some_view_id"
    direction: DOWN
```
