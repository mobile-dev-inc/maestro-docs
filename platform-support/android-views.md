# Android - Views

<figure><img src="../.gitbook/assets/android (1).png" alt=""><figcaption></figcaption></figure>

Maestro fully supports native Android apps. Maestro tests can also run on real hardware devices.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

## Interacting with views by text

Any view with a `text` property can be tapped on:

```xml
<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Hello World" />
```

Can be tapped in the following way:

```yaml
tapOn: Hello World
```

## Interacting with views by id

Views can be accessed by their ids. For example:

```xml
<Button
    android:id="@+id/myButton"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Hello World" />
```

Can be tapped in the following way:

```yaml
- tapOn:
    id: myButton
```

## Interacting with views by contentDescription

`contentDescription` field is surfaced as text property and can be interacted in the same way as any view containing `text`:

```xml
<ImageView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:contentDescription="Hello World" />
```

This view can then be tapped using the following command:

```yaml
- tapOn: Hello World
```

## Known Limitations

1. Unicode text **input** is not yet currently supported. Though views that have unicode in them can still be interacted with.
