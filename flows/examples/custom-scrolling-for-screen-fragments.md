# Custom scrolling for screen fragments

Maestro’s native [`scrollUntilVisible`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/scrolluntilvisible) is a powerful tool, but it works in a specific way:

1. Checks for the elemented defined by the selector.
2. Swipe up from the center of the screen.
3. Return to step 1.

While this works for most full-screen lists, it fails in apps where only a specific part of the screen is scrollable, such as a bottom sheet, a small side-scrolling widget, or a fragmented UI where the top half is static. If the center of your screen isn't scrollable, the native command will simply tap a static element repeatedly.

This example shows you how to build a scrolling logic that swipes exactly where you need it to.

{% hint style="info" %}
#### **Credits**

This issue was first reported by the developers at Amicara, who were facing difficulties scrolling through complex, fragmented layouts.

<p align="center"><img src="../.gitbook/assets/image.png" alt="" data-size="original"></p>
{% endhint %}

### The workflow

To bypass the center-swipe limitation, we recreate the scrolling logic manually using a loop. Instead of letting Maestro decide where to swipe, we define specific screen coordinates to ensure the swipe happens within the scrollable container.

#### 1. Reusable scroll Flow

This subflow (e.g., `scroll_fragment.yaml`) receives the `TARGET_ID` from the parent Flow. It continues to swipe in a restricted area of the screen until the target element is discovered.

```yaml
# scroll_fragment.yaml
# Custom scrolling for targeted screen areas
# Required Env: TARGET_ID (The resource id of the element to find)

# Step 1: Initialize the state
# Use a flag to track if we've found our target yet
- evalScript: ${output.foundElement = 0}

# Step 2: Immediate check
# Before we start moving, let's see if the element is already there
- runFlow:
    when:
      visible:
        id: "${TARGET_ID}"
    commands:
      - evalScript: ${output.foundElement = 1}

# Step 3: The targeted loop
# We continue swiping in the bottom region until foundElement becomes 1
- repeat:
    while:
      true: ${output.foundElement == 0}
    commands:
      # We swipe from 90% down the screen to 75% down the screen.
      # This keeps the interaction strictly within the bottom fragment.
      - swipe:
          start: 50%, 90%
          end: 50%, 75%
      
      # Check again after the movement
      # If the element is visible, we stop the loop
      - runFlow:
          when:
            visible:
              id: "${TARGET_ID}"
          commands:
            - evalScript: ${output.foundElement = 1}
```

This implementation gives you full control over the scroll mechanics. In the `swipe` command, using percentages such as 90% and 75% ensures consistent behavior across different device sizes. By targeting the lower portion of the screen, you avoid accidentally interacting with static headers or non-scrollable hero sections. Additionally, the search flag (`${output.foundElement}`) acts as a bridge between the `runFlow` step, which checks visibility, and the `repeat` loop, which controls the scrolling action.

{% hint style="success" %}
#### Adapt it to your needs

If the static area differs in your app, adjust the swipe command configuration to suit your needs.
{% endhint %}

{% hint style="success" %}
#### Preventing infinite swiping

While not shown in this basic snippet, you can easily add a counter to the `repeat` loop to throw an error if the element isn't found after 10 or 20 swipes, preventing your test from hanging indefinitely.
{% endhint %}

#### 2. Implementation

To use this helper in your main Flow, call it with `runFlow` and pass the `TARGET_ID` of the element you need to find as an environment variable.

```yaml
# main_test.yaml
- tapOn: "Open Settings"

# Find a specific setting at the bottom of a scrollable fragment
- runFlow:
    file: ../utils/scroll_fragment.yaml
    env:
      TARGET_ID: "logout_button"

# Once the subflow finishes, the element is confirmed visible
- tapOn:
    id: "logout_button"
```

#### Related content

Explore the following documentation pages if some of the concepts used in this example are not clear for you:

* [swipe](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/swipe "mention"): Learn how to use coordinates, durations, and percentages to move around the screen.
* [loops.md](../flow-control-and-logic/loops.md "mention"): Understand the difference between looping a fixed number of times vs. looping based on a condition.
