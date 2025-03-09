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
- evalScript: ${output.foundElement = 0}

# Check if it's already visible
- runFlow:
    when:
      visible:
        id: "the_thing_we_want"
    commands:
      - evalScript: ${output.foundElement = 1}

# Loop until found
- repeat:
    while:
      true: ${output.foundElement == 0}
    commands:
      # Swipe up, from 90% down the screen to 75% down the screen
      - swipe:
          start: 50%, 90%
          end: 50%, 75%
      # Check if it's visible yet
      - runFlow:
          when:
            visible:
              id: "the_thing_we_want"
          commands:
            - evalScript: ${output.foundElement = 1}
```
