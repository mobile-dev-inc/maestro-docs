# inputText

Inputs text (regardless of whether any text field is currently focused or not)

```yaml
- inputText: "Hello World"
```

{% hint style="warning" %}
Unfortunately unicode characters are not supported yet. Follow the [GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/146) for status updates.
{% endhint %}

### Input random text

There are several convenience methods for entering a random text input:

```yaml
- inputRandomEmail       # Enters a random Email address
- inputRandomPersonName  # Enters a random person name
- inputRandomNumber      # Enters a random integer number
- inputRandomText        # Enters random unstructured text
```
