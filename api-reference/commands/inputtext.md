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
- inputRandomEmail       # Enters a random Email address
- inputRandomPersonName  # Enters a random person name
- inputRandomNumber      # Enters a random integer number
- inputRandomText        # Enters random unstructured text
```

#### Length

You can pass length as argument for `Number` and `Text`

```yaml
- inputRandomNumber:
    length: 10  #(default: 8)
- inputRandomText:
    length: 10  #(default: 8)
```

#### Re-using random input

To access and re-use your random input, you can use the `copyTextFrom` function, as shown in the example below.

```yaml
- inputRandomText
- copyTextFrom:
    id: MyTextInput
...
- assertVisible: ${maestro.copiedText}
or with regex
- assertVisible: ${'.*' + maestro.copiedText + '$'}
or tapOn
- tapOn: ${maestro.copiedText}
```
