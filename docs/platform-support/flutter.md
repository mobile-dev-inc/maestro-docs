# Flutter

<figure><img src="../.gitbook/assets/flutter.png" alt=""><figcaption></figcaption></figure>

Maestro supports Flutter

Commands such as `tapOn` provide you with ways to select these widgets based on text or semantic labels.

## Interacting with Widgets by Text

Maestro can interact with widgets that have some displayed text (`data` in the Text widget, `hintText` in the TextField).

#### Example: Tap on a InkWell widget

Given an `InkWell` widget with a `Text` widget child:

```dart
InkWell(
    child: const Text('Open Browser'),
    onTap: () => launch('')
)
```

The following command will tap on the InkWell widget:

```yaml
- tapOn: "Open Browser"
```

#### Example: Tap on TextFormField

For the following widget:

```dart
TextFormField(
    decoration: const InputDecoration(
        border: UnderlineInputBorder(), 
        labelText: 'Enter your username'
    )
)
```

The following command will tap on the `TextFormField`:

```yaml
- tapOn: "Enter your username"
```

## Interacting with Widgets by semantic label

Views can be decorated with a [Semantics](https://api.flutter.dev/flutter/widgets/Semantics-class.html) widget that will attach a semantic label that in turn can be used to locate a view

```dart
Semantics(
    label: "My Label",
    child: SomeView()
)
```

`SomeView` can then be located using the label:

```yaml
- tapOn: ".*My Label.*"
```

#### semanticLabel property

Some widgets can be interacted with via `semanticLabel` property directly. For the following widget:

```dart
FloatingActionButton(
   onPressed: _incrementCounter,
   child: const Icon(Icons.add, semanticLabel: "fabAddIcon"),
)
```

The following command will tap on the `FloatingActionButton`

```yaml
- tapOn: "fabAddIcon"
```

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

## Known Limitations

There are known limitations

1. In cases where there are both `semanticLabel` and text label, the `semanticLabel` takes precedence. It's recommended to use `maestro studio` to identify accessibility labels.
2. Interaction on the basis of `key` is currently not possible.
3. Maestro cannot be used to test desktop or web apps (yet).
