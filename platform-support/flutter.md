# Flutter

<figure><img src="../.gitbook/assets/flutter.png" alt=""><figcaption></figcaption></figure>

Flutter is a first class citizen for Maestro. It can test both pure and hybrid (i.e [add-to-app](https://docs.flutter.dev/add-to-app)) Flutter mobile apps.

## Interacting with widgets by semantics label

Maestro can interact with widgets that have semantics information attached. By default, this includes all widgets that display text (`data` in the Text widget, `hintText` in the TextField, and so on). You can also attach semantics information to any widget using Flutter's [Semantics widget](https://api.flutter.dev/flutter/widgets/Semantics-class.html).

### Example: Tap on a widget

Given an `InkWell` widget with a `Text` widget child:

{% code fullWidth="false" %}
```dart
InkWell(
  child: Text('Open Browser'),
  onTap: () => launch('https://mobile.dev'),
)
```
{% endcode %}

The following command will tap on it:

```yaml
- tapOn: Open Browser
```

***

Some widget, such as `Icon`, don't have implicit semantics. In such cases you can often pass a `semanticLabel`:

```dart
FloatingActionButton(
  onPressed: _incrementCounter,
  child: Icon(Icons.add, semanticLabel: 'fabAddIcon'),
)
```

Then the `FloatingActionButton` can be interacted with using the following command:

```yaml
- tapOn: fabAddIcon
```

{% hint style="info" %}
The `Icon` widget simply creates a `Semantics` widget itself – [see the source](https://github.com/flutter/flutter/blob/3.16.0/packages/flutter/lib/src/widgets/icon.dart#L303-L314).
{% endhint %}

***

Finally, you can wrap any widget with [Semantics](https://api.flutter.dev/flutter/widgets/Semantics-class.html):

```dart
Semantics(
  label: 'funky yellow box',
  child: Container(
    color: Colors.yellow,
    width: 100,
    height: 100,
  ),
)
```

```yaml
- tapOn: funky yellow box
```

### Example: Enter text in a widget

To enter text in the following text field widget:

```dart
TextField(
  decoration: InputDecoration(
    border: UnderlineInputBorder(), 
    labelText: 'Enter your username',
  ),
)
```

Use this command:

```yaml
- tapOn: Enter your username
- inputText: charlie_root
```

### Example: Assert a widget is visible

```dart
Text(
  'Welcome back, dear $fullName! 👋🎉',
  semanticsLabel: 'Welcome back, dear $fullName!',
),
```

```yaml
- assertVisible: Welcome back, dear Test User!
```

{% hint style="info" %}
In cases where both `semanticLabel` and text label are provided (like above), the `semanticLabel` takes precedence. It's recommended to use `maestro studio` in such cases to easily identify what label to use.
{% endhint %}

## Interacting with widgets by semantic identifier

When your app grows, testing often becomes harder.

Maybe the app gets multi-language support, and now you have to decide on the language in which you test it. Maybe some of the strings displayed are non-static (e.g. becase of A/B tests). And the sheer number of screens makes tests harder to maintain.

When you start facing these problems, you should consider using the **accessibility identifier** instead of semantics labels.

{% hint style="info" %}
This is a new feature that [we contributed to Flutter](https://github.com/flutter/engine/pull/47961) to make it easier to test apps made with it. It's available on the stable channel since Flutter 3.19 (released on February 15th, 2024). To use it, upgrade to the latest stable Flutter release:

```
flutter channel stable
flutter upgrade
```
{% endhint %}

### Example: Tap on a widget by semantics identifier

```dart
Semantics(
  identifier: 'signin_button',
  child: ElevatedButton(
    onPressed: _signIn,
    child: Text('Sign in'),
  ),
)
```

```yaml
- tapOn:
    id: signin_button
```

### Example: Enter text in a widget by semantics identifier

```dart
Semantics(
  identifier: 'username_textfield',
  child: TextField(
    decoration: InputDecoration(
      border: UnderlineInputBorder(), 
      labelText: 'Enter your username',
    ),
  ),
)
```

```yaml
- tapOn:
    id: username_textfield
- inputText: charlie_root
```

## Good practices

Let's say you have a `FancyButton` widget in your app. These buttons are important for you, and you want to ensure they always have an accessibility identifier assigned so they can be reliably interacted with using Maestro. The code sample below requires all callers of `FancyButton` to pass an accessibility identifier:

```dart
class FancyButton extends StatelessWidget {
 FancyButton({
    super.key,
    required this.identifier,
    required this.onPressed,
  });

  final String identifier;
  final VoidCallback onPressed;

  @override
  Widget build(BuildContext context) {
    return Semantics(
      identifier: identifier,
      child: RawMaterialButton(
        onPressed: onPressed,
        // ...
      ),
    );
  }
}
```

This also has the benefit of reducing widget nesting at the call site:

```dart
FancyButton(
  identifier: 'buy_premium',
  onPressed: _buyPremium,  
)

// instead of:

Semantics(
  identifier: 'buy_premium',
  FancyButton(
    onPressed: _buyPremium,
  ),
)
```

Of course, there's always danger of a developer accidentally not using the `FancyButton` widget and defering to the built-in `ElevatedButton`. To combat that, we recommend setting up lint rules that forbid using `ElevatedButton` and enforce replacing it with a `FancyButton` instead. For example you can use [the leancode_lint package](https://pub.dev/packages/leancode_lint) with the following configuration in `analysis_options.yaml`:

```yaml
include: package:leancode_lint/analysis_options.yaml

custom_lint:
  rules:
    - use_design_system_item:
      FancyButton:
        - instead_of: ElevatedButton
          from_package: flutter
          
analyzer:
  plugins:
    - custom_lint
```

## Why not Flutter keys?

Flutter widget keys cannot be used in Maestro because there's no linkage between widget keys and Flutter's accessibility bridge system. This makes using Keys impossible since Maestro is accessibility-tree based.

Also, Flutter API docs for the [Key class](https://api.flutter.dev/flutter/foundation/Key-class.html) and [Widget.key field](https://api.flutter.dev/flutter/widgets/Widget/key.html) say it's for "controlling how one widget replaces another (e.g. in a list)". Keys are just not a mechanism for assigning unique IDs to widgets for testing purposes.

We strongly recommend making your app accessible (not just for UI tests, but for all of your users with different needs). When testing at scale, you should also consider using an accessibility identifier.

Here's also a little trick that you may find useful if you really want to use keys in Maestro (using the `FancyButton` example from above):

```dart
class FancyButton extends StatelessWidget {
  FancyButton({
    required String key,
    required this.onPressed,
  })  : _key = key,
        super(key: ValueKey(key));

  final String _key;
  final VoidCallback onPressed;

  @override
  Widget build(BuildContext context) {
    return Semantics(
      identifier: _key,
      child: RawMaterialButton(
        onPressed: onPressed,
        // ...
      ),
    );
  }
}
```

Callers are required to pass a string key:

```dart
FancyButton(
  key: 'unlock_reward',
  onPressed: _unlockReward,
)
```

And you can easily interact with the widget using Maestro:

```yaml
- tapOn:
    id: unlock_reward
```

## Known Limitations

Maestro cannot be used to test Flutter Desktop or Flutter Web apps (yet).
