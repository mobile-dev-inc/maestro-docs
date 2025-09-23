---
description: >-
  Test SwiftUI apps with Maestro. Generate flows via Studio, interact with text
  fields and accessibility labels, and validate real-world scenarios.
---

# iOS - SwiftUI

<figure><img src="../.gitbook/assets/swiftui.png" alt=""><figcaption></figcaption></figure>

Maestro fully supports iOS apps that use SwiftUI.\
\
In addition to iOS UIKit apps it is possible to write maestro flows for the apps that are written in SwiftUI. For showcasing the capabilities of maestro two open-source apps were picked - [Food Truck app](https://github.com/artem888/sample-food-truck) from WWDC22 and [SwiftUI Kit app](https://github.com/artem888/SwiftUI-Kit) that demonstrates different SwiftUI components in a storybook manner.

### Basic flow

First lets start with some basic flow for FoodTruck app. Almost every SwiftUI native element is identifiable with maestro studio. For instance here is how the first step of [first\_flow.yaml](https://github.com/artem888/sample-food-truck/blob/main/.mobiledev/first_flow.yaml) was generated:

<figure><img src="../.gitbook/assets/Screenshot 2023-01-12 at 21.48.45.png" alt=""><figcaption></figcaption></figure>

`index: 0` can be omitted and the first step of the flow looks like that:

```yaml
- tapOn:
    text: "New Orders"
```

All the other steps in this flow were generated the same way, following examples provided by `maestro studio`.\
\
The [flow](https://github.com/artem888/sample-food-truck/blob/main/.mobiledev/text_input.yaml) itself navigates to order details screen, marks that an order is completed and finally asserts that the order is not in the list anymore, which can be considered as real-world use-case scenario.

### Text Input

[Here is an example](https://github.com/artem888/sample-food-truck/blob/main/.mobiledev/text_input.yaml) of a flow that relies on the text input.

```yaml
// First typing on the element that has a prewritten placeholder text:
- tapOn:
    text: "New Donut"
    index: 1

// Erasing the text completely
- eraseText

// input new contents for the TextField
- inputText: "Test Donut"
```

There is a better way to focus on a TextField rather than watching on its contents - accessibility id / label, which is explained in the next section.

### Accessibility info

The best practice to write reliable flows with maestro for SwiftUI is to assign `accessibilityIdentifier` or `accessibilityLabel` for UI element that needs to be accessed.

Here is the code modification that needed to be done for the Food Truck to make `tapOn` work with id:

```swift
NavigationLink(value: Panel.donutEditor) {
	Label("Donut Editor", systemImage: "slider.horizontal.3")
}.accessibilityIdentifier("donut_editor")
```

Corresponding tap command on maestro side would now look like that:

```yaml
- tapOn:
    id: "donut_editor"
```

Full flow can be found [here](https://github.com/artem888/sample-food-truck/blob/main/.mobiledev/accessibility_label.yaml).\
\
maestro translates `accessibilityIdentifier` to `id` while `accessibilityLabel` is translated to `text`. When an element has both some text content and `accessibilityLabel` assigned the latter will be picked as a value for `text` by maestro framework.

### System menus / dialogs

[The following flow](https://github.com/artem888/SwiftUI-Kit/blob/master/.mobiledev/buttons.yaml) demonstrates how to interact with different types of native popups / dialogs / context menus etc. To simplify an access to the elements `accessibilityIdentifier` was used again, whenever possible.

### System controls

[The following flow](https://github.com/artem888/SwiftUI-Kit/blob/master/.mobiledev/controls.yaml) demonstrates how to interact with native SwiftUI controls like Toggle, Picker, Segmented Picker. The best practice here is to give unique `accessibilityIdentifier` values to individual elements that represent some value in a list.

### Switching between different apps

Switching between different apps during the same flow is also supported by maestro. [The following flow](https://github.com/artem888/SwiftUI-Kit/blob/master/.mobiledev/link.yaml) opens url in Safari and then returns to the main app (SwiftUI-Kit) that was previously launched.

```yaml
- tapOn:
    id: "breadcrumb"
```

<div align="left"><figure><img src="../.gitbook/assets/Simulator Screen Shot - iPhone 14 - 2023-01-12 at 22.31.14 (2) (1).png" alt=""><figcaption></figcaption></figure></div>

breadcrumb is an accessibility id\
of the “Back to SwiftUI app”\
button on the screenshot below, which was also found with a help of `maestro studio`

### Known issues:

* Hierarchy for some elements is not returned (i.e. **WheelPickerStyle**)
* When **Toggle** is initialized with text, its accessibility element is a union of a text and toggle
* Sometimes only one of accessibilityLabel / accessibilityIdentifier (i.e. **Link**)
* Sometimes List / Group elements are not assigning accessibility ids / labels correctly (i.e `SectionView { Group { Menu } }`)

{% content-ref url="ios-swiftui.md" %}
[ios-swiftui.md](ios-swiftui.md)
{% endcontent-ref %}
