---
description: >-
  Test iOS UIKit apps with Maestro. Interact via text, accessibility labels or
  ids.
---

# iOS - UIKit

<figure><img src="../.gitbook/assets/ios.png" alt=""><figcaption></figcaption></figure>

Maestro fully supports native iOS UIKit apps.

## Interacting with views by text

Any view with text content can be tapped on, i.e.:

```swift
let button = UIButton()
button.setTitle("Hello World", for: .normal)
```

Can be tapped in the following way:

```
tapOn: Hello World
```

## Interacting with views by accessibility labels

Views can be accessed by their accessibility labels. For example:

```swift
let button = UIButton()
button.accessibilityLabel = "Hello World button"
```

Can be tapped in the following way:

```
tapOn: Hello World button
```

**NB!** maestro translates `accessibilityIdentifier` to `id` while `accessibilityLabel` is translated to `text`. When an element has both some text content and `accessibilityLabel` assigned the latter will be picked as a value for `text` by maestro framework.

## Interacting with views by accessibility ids

Views can be accessed by their accessibility ids. For example:

```swift
let button = UIButton()
button.accessibilityIdentifier = "hello_world_id"
```

Can be tapped in the following way:

```
- tapOn:
    id: "hello_world_id"
```

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### Known Limitations

1. Maestro can't interact with real iOS devices yet. Only Simulator is supported at the moment.
