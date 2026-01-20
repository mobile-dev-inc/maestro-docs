---
description: >-
  Enter text into fields in Maestro, including random emails, names, or numbers
  with length.
---

# inputText

Inputs text (regardless of whether any text field is currently focused or not)

```yaml
- inputText: "Hello World"
```

{% hint style="warning" %}
Unfortunately unicode characters are not supported yet in Android platform. Follow the [GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for status updates.
{% endhint %}

### Input random text

There are several convenience methods for entering a random text input:

```yaml
- inputRandomEmail         # Enters a random Email address
- inputRandomPersonName    # Enters a random person name
- inputRandomNumber        # Enters a random integer number
- inputRandomText          # Enters random unstructured text
- inputRandomCityName      # Enters a random city name, worldwide
- inputRandomCountryName   # Enters the name of a random country
- inputRandomColorName     # Enters a random colour. Might be multiple words.
```

Note: Since Maestro v2.0, the implementation behind the random commands was changed to use [DataFaker](https://www.datafaker.net/), which gives a much wider spread of random data than was available in Maestro v1.x.

#### Length

You can pass length as argument for `Number` and `Text`

```yaml
- inputRandomNumber:
    length: 10  #(default: 8)
- inputRandomText:
    length: 10  #(default: 8)
```

#### Re-using random input

To access and re-use your random input, you can use the [copyTextFrom](copytextfrom.md) function, as shown in the example below.

```yaml
- tapOn:
    id: MyTextInput
- inputRandomText
- copyTextFrom:
    id: MyTextInput

- tapOn: 'Submit' # Assumes a form where the input will be displayed on the next screen

- assertVisible: ${maestro.copiedText}
# or with regex
- assertVisible: ${'.*' + maestro.copiedText + '$'}
# or tapOn
- tapOn: ${maestro.copiedText}
```
