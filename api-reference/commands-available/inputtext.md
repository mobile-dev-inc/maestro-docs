---
description: Type text into focused input fields with optional keyboard handling.
---

# inputText

the `inputText` command inputs a specified text string. This command works even if no text field is focused.

### Syntax

You can use the shorthand string syntax for quick inputs:

```yaml
- inputText: "string"
```

You can also use the expanded syntax to include the label:

```yaml
- inputText:
    text: "user@example.com"
    label: "Input the test system username"
```

The `label` parameter provides real-world context in your test reports, making it clear what specific data is being entered during that step.

### Unicode input on Android

Since Maestro 2.7.0, `inputText` supports non-ASCII text on Android, including accented letters, non-Latin scripts such as Arabic, Chinese, Japanese and Korean, and emoji. This works both locally and in Maestro Cloud. Earlier versions fail with a `Unicode character input is not supported` error.

```yaml
- tapOn: "Search"
- inputText: "こんにちは世界"
- eraseText
- inputText: "Hello 👋 World 🌍"
```

If the text contains any non-ASCII character, Maestro enters it differently from ASCII-only text:

* **The text is inserted all at once.** It is not typed as a series of key presses, which often makes it faster than typing ASCII text. This applies to the whole string, so `"Hello 👋"` is inserted in one go even though it is mostly ASCII.
* **A text field must be focused.** Maestro switches to its own input method and inserts the text into the focused field. If no field is focused, the command fails after about 5 seconds with `No active input connection`. Tap the field first, as shown above. ASCII-only text does not need a focused field.
* **The keyboard is switched temporarily.** Maestro sets its own input method on the device, then restores the original keyboard once the text is entered.

### Random text input commands

Maestro provides several commands to input randomly generated data. These commands use the [DataFaker](https://www.datafaker.net/) library.

| Command                  | Description                      |
| ------------------------ | -------------------------------- |
| `inputRandomEmail`       | Inputs a random email address.   |
| `inputRandomPersonName`  | Inputs a random person's name.   |
| `inputRandomNumber`      | Inputs a random integer.         |
| `inputRandomText`        | Inputs random unstructured text. |
| `inputRandomCityName`    | Inputs a random city name.       |
| `inputRandomCountryName` | Inputs a random country name.    |
| `inputRandomColorName`   | Inputs a random color name.      |

#### Parameters for random text commands

You can specify the length for certain random input commands.

| Parameter | Type      | Applicable Commands                       | Description                                                                   |
| --------- | --------- | ----------------------------------------- | ----------------------------------------------------------------------------- |
| `length`  | `integer` | `inputRandomNumber` and `inputRandomText` | Specifies the number of digits or characters to generate. The default is `8`. |

### Usage examples

You can use the `inputText` command to add a specific string:

```yaml
- inputText: "Hello World"
```

You can also input a random number or text with a specific length:

```yaml
- inputRandomNumber:
    length: 9  
- inputRandomText:
    length: 11  
```

#### Reuse a random value in an assertion

This example inputs a random string, copies it to a variable, and then asserts that the copied text is visible on the next screen.

```yaml
- tapOn:
    id: MyTextInput
- inputRandomText
- copyTextFrom:
    id: MyTextInput
- tapOn: 'Submit'
- assertVisible: ${maestro.copiedText}
```

In this example, `copyTextFrom` stores the copied text in the `copiedText` variable. This value is then used by `assertVisible` to verify that the generated text appears on the new screen after tapping the **Submit** button.

#### Use variables

You can input dynamic data stored in variables or the results of JavaScript expressions.

```yaml
# Input text from an environment variable or previous output
- inputText: ${USER_EMAIL}

# Input using complex logic
- inputText: ${'testuser_' + Math.floor(Math.random() * 1000)}
```

{% hint style="warning" %}
On iOS simulators, `inputText` can fail on password fields (`secureTextEntry`) because of iOS Password AutoFill. See [Known issues](https://app.gitbook.com/s/htfynyR39703f5pJOF1P/troubleshooting/known-issues) for workarounds.
{% endhint %}

### Related commands

* [copytextfrom.md](copytextfrom.md "mention")
