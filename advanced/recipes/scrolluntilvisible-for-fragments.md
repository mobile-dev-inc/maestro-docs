# scrollUntilVisible for fragments

Our friends at Amicara hit a problem with their app that Maestro couldn't natively solve. They wanted to use `scrollUntilVisible`, but it wasn't working for them.

Now, under the hood, scrollUntilVisible works like this:

1. Checks for the visibility of the element described by the selector
2. Swipe up from the center of the screen
3. Go to step 1

Now, in Amicara's app, scrolling from the middle wouldn't work - only the bottom half of the app had scrollable elements.

<figure><img src="../../.gitbook/assets/image (8).png" alt="" width="375"><figcaption></figcaption></figure>

Working with their test developers and other folks in the community, we developed a new version of scrollUntilVisible through native Maestro commands.



```yaml
# Initialize state
- evalScript: ${output.foundElement = false}
- evalScript: ${output.retries = 0}

# Check if element is already visible
- runFlow:
    when:
      visible:
        id: "the_thing_we_want"
    commands:
      - evalScript: ${output.foundElement = true}

# Loop until element is found or retries exhausted
- repeat:
    while:
      true: ${!output.foundElement && output.retries < 10}
    commands:
      # Swipe vertically in the bottom portion of the screen (fragment-safe)
      - swipe:
          start: 50%, 90%
          end: 50%, 75%
      
      # Wait for UI / animation to settle
      - waitForAnimationToEnd

      # Check visibility again
      - runFlow:
          when:
            visible:
              id: "the_thing_we_want"
          commands:
            - evalScript: ${output.foundElement = true}

      # Increment retry counter
      - evalScript: ${output.retries += 1}

# Final assertion to ensure the element is visible
- assertVisible:
    id: "the_thing_we_want"
```
