---
description: Find and use the last matching index for a given selector in Maestro
---

# Get the last matching element

In Maestro you can choose to target the n<sup>th</sup> element matching a selector using [indexes](../../api-reference/selectors.md#selecting-one-view-among-many-similar), e.g.

```
- tapOn:
    text: Add to Basket
    index: 2   # 3rd item, indexes start at 0
```

What if you want the last item on the screen, but don't know how many there are? That's harder, and requires an algorithmic approach.

This helper comes courtesy of [Ben Sussman](https://github.com/bensussman) from Pomelo Care, probably best used as a subflow, loops through visible elements for a given selector, and returns the index of the last matching element.&#x20;

```
# A reusable helper to find the last element matching a given selector.
# Usage:
#   - runFlow:
#       file: utils/findLastElement.yml
#       env:
#         SELECTOR_TYPE: "id"          # Supported: "id", "text"
#         SELECTOR_VALUE: "my_button"  # The actual selector value
#
# After running, the last element index will be available as ${output.lastElementIndex}
#
# Example usage:
#
# - runFlow:
#     file: ../utils/findLastElement.yml
#     env:
#       SELECTOR_TYPE: "text"
#       SELECTOR_VALUE: "Add to Basket"
# - tapOn:
#   text: "Add to Basket"
#   index: ${output.lastElementIndex}

# Initialize variables (always reset for fresh execution)
- evalScript: ${output.lastElementIndex = -1}
- evalScript: ${output._findLastElement_complete = false}


# Validate SELECTOR_TYPE
- runFlow:
    when:
      true: ${SELECTOR_TYPE != "id" && SELECTOR_TYPE != "text"}
    commands:
      - evalScript: |
          throw new Error("Invalid SELECTOR_TYPE: " + SELECTOR_TYPE + ". Must be 'id' or 'text'");

# Find the last element by iterating through indices
- repeat:
    while:
      true: ${!output._findLastElement_complete}
    commands:
      # Check if element exists at current index (id selector)
      - runFlow:
          when:
            true: ${SELECTOR_TYPE == "id"}
          commands:
            - runFlow:
                when:
                  visible:
                    id: "${SELECTOR_VALUE}"
                    index: ${output.lastElementIndex + 1}
                commands:
                  # Element found, update index and continue
                  - evalScript: ${output.lastElementIndex = output.lastElementIndex + 1}
            - runFlow:
                when:
                  notVisible:
                    id: "${SELECTOR_VALUE}"
                    index: ${output.lastElementIndex + 1}
                commands:
                  # Element not found, we're done
                  - evalScript: ${output._findLastElement_complete = true}

      # Check if element exists at current index (text selector)
      - runFlow:
          when:
            true: ${SELECTOR_TYPE == "text"}
          commands:
            - runFlow:
                when:
                  visible:
                    text: "${SELECTOR_VALUE}"
                    index: ${output.lastElementIndex + 1}
                commands:
                  # Element found, update index and continue
                  - evalScript: ${output.lastElementIndex = output.lastElementIndex + 1}
            - runFlow:
                when:
                  notVisible:
                    text: "${SELECTOR_VALUE}"
                    index: ${output.lastElementIndex + 1}
                commands:
                  # Element not found, we're done
                  - evalScript: ${output._findLastElement_complete = true}

# Validate that at least one element was found
- runFlow:
    when:
      true: ${output.lastElementIndex == -1}
    commands:
      - evalScript: |
          throw new Error("No elements found matching selector: " + SELECTOR_TYPE + '="' + SELECTOR_VALUE + '"');>
```
