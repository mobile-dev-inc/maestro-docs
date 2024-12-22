# launchApp



To launch the app under test, simply write:

```
- launchApp
```

To launch an arbitrary app with a given id (package name on Android, bundle id on iOS), do:

```yaml
- launchApp: appId
```

If you need to clear the app state before launching the app, specify a `clearState` flag

```yaml
- launchApp:
    appId: "com.example.app"
    clearState: true
    clearKeychain: true   # optional: clear *entire* iOS keychain
    stopApp: false # optional (true by default): stop the app before launching it
    permissions: { all: deny } # optional: by default all permissions are allowed,
                               # even if clearState: true is passed
```

If you want to test with a permission with a specific value, specify a permissions argument

```yaml
- launchApp:
    permissions:
        notifications: unset # notification permission is unset
        android.permission.ACCESS_FINE_LOCATION: deny # Android fine location permission is denied
```

### Launch Arguments

You can send launch arguments while launching the app for both iOS and Android.&#x20;

#### Sending launch arguments

Arguments allow sending **String**, **Boolean**, **Double,** and **Integer**. All other data types are by default passed as a String.

```yaml
- launchApp:
    appId: "com.example.app"
    arguments: 
       foo: "This is a string"
       isFooEnabled: false
       fooValue: 3.24
       fooInt: 3
```

#### Receiving arguments on Android

```kotlin
intent.extras?.getBoolean("isFooEnabled")?.let {
    // Do something with isFooEnabled
}

intent.extras?.getString("foo")?.let {
    // Do something with foo
}
```

#### Receiving arguments on iOS

```swift
if ProcessInfo.processInfo.arguments.contains("isFooEnabled") {
    // Do something with isFooEnabled
}

// By default all the values received here would be string
let standardDefaultsDict = UserDefaults.standard.dictionaryRepresentation()
let foo = (standardDefaultsDict["foo"] as? String) ?? "defaultValue"
```

#### Receiving arguments in React Native

```typescript
import { LaunchArguments } from 'react-native-launch-arguments'

export const isFooEnabled = () => {
  try {
    const foo = LaunchArguments.value().isFooEnabled
    return !!foo
  } catch (e) {
    return false
  }
}
```

#### Receiving arguments in Flutter

```dart
import 'package:flutter_launch_arguments/flutter_launch_arguments.dart';

Future<void> getArguments() async {
  final fla = FlutterLaunchArguments();

  final foo = await fla.getString('foo');
  final isFooEnabled = await fla.getBool('isFooEnabled');
  final fooValue = await fla.getDouble('fooValue');
  final fooInt = await fla.getInt('fooInt');
}
```