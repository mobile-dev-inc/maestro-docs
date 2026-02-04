---
description: Tap on UI elements by text, ID, or coordinates with optional repeat and delay.
---

# tapOn

The `tapOn` command performs a tap gesture on a UI element or a specific coordinate on the screen. It is the most common interaction command in Maestro.

{% hint style="info" %}
#### Perform a long press

Use the [`longPressOn`](longpresson.md) command to perform a long press. It accepts the same selectors and parameters as `tapOn`.
{% endhint %}

### Parameters

You can specify the target element using a shorthand text selector or a map containing a selector and optional interaction parameters.

<table><thead><tr><th width="202">Parameter</th><th width="135">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>selector</code></td><td>String or Map</td><td><strong>Required.</strong> The element to tap. Use a string for a shorthand text selector (e.g. <code>"My Text"</code>). For other selectors or to add parameters, use a map. See the Selectors documentation for a full list.</td></tr><tr><td><code>point</code></td><td>String</td><td>A specific coordinate to tap on the screen or within a selected element. Use relative percentages (e.g. <code>"50%,50%"</code>) or absolute pixel values (e.g. <code>"100,200"</code>).</td></tr><tr><td><code>repeat</code></td><td>Integer</td><td>The number of times to repeat the tap.</td></tr><tr><td><code>delay</code></td><td>Integer</td><td>The delay in milliseconds between each tap when using <code>repeat</code>. Defaults to <code>100</code>.</td></tr><tr><td><code>retryTapIfNoChange</code></td><td>Boolean</td><td>If <code>true</code>, Maestro retries the tap if the UI hierarchy does not change after the initial tap. This is useful for handling early taps before the UI is fully responsive.</td></tr><tr><td><code>waitToSettleTimeoutMs</code></td><td>Integer</td><td>The maximum time in milliseconds that Maestro waits for the screen to settle before executing the next command. This is a best-effort timeout; Maestro does not interrupt core operations to honor it.</td></tr></tbody></table>

### Usage examples

The following examples demonstrate how to use the `tapOn` and `longPressOn` commands.

#### Tap an element by text or ID

The fastest way to interact with your app is via visible text or technical identifiers. This example shows the shorthand for tapping an element by its visible text.

```yaml
- tapOn: "My text"
```

This example uses the `id` selector to tap an element.

```yaml
- tapOn:
    id: "your.view.id"
```

#### Repeat a tap

If you need to tap the same element several times in a row, use `repeat`. This option is useful, for example, when you need to increase the value of a counter.

If you need to wait for the animation to finish before executing the next tap, use `delay`. This example taps the button five times with a 200 ms delay between each tap.

```yaml
- tapOn:
    id: "plus_button"
    repeat: 5
    delay: 200
```

#### Retry a tap if the UI is unresponsive

If a tap is ignored because the target was not ready yet or an animation is still playing, use `retryTapIfNoChange`. This example retries the tap if the UI does not change after the first attempt.

```yaml
- tapOn:
    id: "someId"
    retryTapIfNoChange: true
```

#### Tap a specific coordinate

While element selectors are preferred, you can target specific points on the screen. This example taps the center of the screen.

```yaml
- tapOn:
    point: "50%,50%"
```

This example taps an absolute coordinate on the screen.

```yaml
- tapOn:
    point: "100,200"
```

{% hint style="info" %}
Prefer using element selectors like `id` or `text` over coordinates. Tapping by coordinate can make tests brittle and device-dependent.
{% endhint %}

#### Tap a coordinate within an element

This example finds an element containing specific text and then taps a point near the end of that element.

```yaml
- tapOn:
    text: "A text with a hyperlink"
    point: "90%,50%"
```

#### Full flow example

This example demonstrates a sequence of commands to add a new contact.

```yaml
appId: com.android.contacts
---
- launchApp
- tapOn:
    id: ".*floating_action_button.*" # regex
- inputText: "John"
- tapOn: "Last Name"
- inputText: "Snow"
- tapOn: ".*Save.*"
```

### Related content

Check the related commands:

* [longpresson.md](longpresson.md "mention")
* [doubletapon.md](doubletapon.md "mention")

Or, learn about the different ways to identify elements using [Selectors](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/how-to-use-selectors).
