# inputText

the `inputText` command inputs a specified text string. This command works even if no text field is focused.

```yaml
- inputText: "string"
```

{% hint style="warning" %}
Unicode characters are not supported on Android. See [GitHub issue #146](https://github.com/mobile-dev-inc/maestro/issues/146) for status updates.
{% endhint %}

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

### Related commands

* [copytextfrom.md](copytextfrom.md "mention")
