# Get the last matching element

In Maestro, targeting a specific view is usually straightforward using [indexes](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/selectors/core-selectors). For example, if you want the third **Add to Basket** button, you simply use `index: 2` :&#x20;

```yaml
- tapOn:
    text: Add to Basket
    index: 2   # 3rd item. Indexes start at 0
```

But what if you are testing a dynamic list, like a shopping cart, a message thread, or a photo gallery, where the number of items changes? If you need to interact with the very last item but don't know the total count, you need a more algorithmic approach.

{% hint style="info" %}
#### **Credits**

This clever indexing helper was shared with the community by [Ben Sussman](https://github.com/bensussman) from the team at Pomelo Care.
{% endhint %}

### The workflow

Since Maestro doesn't have a built-in `index: last` selector, you have to find it yourself by iterating through the list. The logic works like a scanning loop:

1. Start at `index:  0`.
2. Check if the element exists at the current index.
3. If it exists, increment the counter and check the next `index`.
4. As soon as an `index` returns `not visible`, you know the previous `index` was the last one.

#### **1. Reusable discovery Flow**

Create a utility subflow (e.g., `utils/find_last_element.yaml`) that will contain all the  scanning loop logic. This subflow will handle the heavy lifting of looping and state management, eventually exporting the correct `index` to your main Flow.

```yaml
# utils/find_last_element.yaml
# Usage: Pass SELECTOR_TYPE ("id" or "text") and SELECTOR_VALUE
# Result: The index is stored in ${output.lastElementIndex}

# Step 1: First, it's necessary to initialize the search state
- evalScript: ${output.lastElementIndex = -1}
- evalScript: ${output._findLastElement_complete = false}

# Step 2: Validate the input type to avoid failures
# Only "id" and "text" selector are supported in this example
- runFlow:
    when:
      true: ${SELECTOR_TYPE != "id" && SELECTOR_TYPE != "text"}
    commands:
      - evalScript: |
          throw new Error("Invalid SELECTOR_TYPE: " + SELECTOR_TYPE + ". Must be 'id' or 'text'");

# Step 3: The Discovery Loop
# Repeat this until you hit an index that doesn't exist.
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
                  # Element not found. The search is done
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
                  # Element not found. The search is done
                  - evalScript: ${output._findLastElement_complete = true}

# Step 4: Final Validation
- runFlow:
    when:
      true: ${output.lastElementIndex == -1}
    commands:
      - evalScript: |
          throw new Error("No elements found matching: " + SELECTOR_VALUE);
```

This script is essentially a linear search algorithm written in Maestro YAML. Here an explanation about core points of this Flow:

* It uses `output` variables to keep track of the counter. Because `evalScript` persists across the Flow execution, we can safely increment the index and use it in the next iteration of the loop.
* By using the `repeat` command with the `while` condition based on a boolean flag (`_findLastElement_complete`, which as initialized as `false`), we can continue searching indefinitely until the list ends, making this compatible with lists of any size.
* In the case an error happen if the script finishes and the index is still `-1`, it throws a JavaScript error. This prevents your test from continuing with a broken state and gives you a clear error message.

#### **2. Implementation**

To use this helper, call it as a subflow and then use the resulting `${output.lastElementIndex}` in your next command. You have to specify the selector type (`id` or `text`) and the value to specify the component.

```yaml
# main_test.yaml
# Find the last "Remove" button in a shopping cart and tap it
- runFlow:
    file: ../utils/find_last_element.yaml
    env:
      SELECTOR_TYPE: "text"
      SELECTOR_VALUE: "Remove"

- tapOn:
    text: "Remove"
    index: ${output.lastElementIndex}
```

### Related content

If you want to explore the building blocks of this algorithmic approach, check out these pages:

* [loops.md](../flow-control-and-logic/loops.md "mention"): Learn the different ways to iterate in Maestro, including `while` loops and count-based loops.
* [javascript-overview.md](../javascript/javascript-overview.md "mention"): Discover how to use JavaScript to manage complex state and logic within your YAML files.
* [how-to-use-selectors.md](../how-to-use-selectors.md "mention"): Review the fundamentals of how Maestro identifies and differentiates between similar UI elements.
