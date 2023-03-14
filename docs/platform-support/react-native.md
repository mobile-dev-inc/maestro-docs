# React Native

<figure><img src="../.gitbook/assets/reactnative.png" alt=""><figcaption></figcaption></figure>

Maestro supports testing React Native screens and apps on both Android and iOS.

### Interacting with a component by Text

Maestro can interact with components that display text.

#### Example: Tap on a Button

For the Button component definition:

```dart
<Button
	title="Go"
	onPress={() => Alert.alert('Success!')}
/>
```

The following command will tap on the Button:

```dart
- tapOn: "Go"
```

### Interaction with a component by testID

Maestro can interact with components that have a testID.

#### Example: Tap on a button with a testID property

For the Button component definition:

```dart
<Button
	title="Go"
  testID="continue"
	onPress={() => Alert.alert('Success!')}
/>
```

The following command will tap on the Button:

```dart
- tapOn:
    id: "continue"
```

### Entering text in a Text Input

#### Example: Enter text into a TextInput.

To input text to a TextInput component, first the component needs to be selected. This can be done using the tapOn command. For the component definition:

```dart
<TextInput placeholder="Change me!" />
```

The following commands will enter "Hello, Maestro!" in the TextInput component:

```dart
- tapOn: "Change me!"
- inputText: "Hello, Maestro!"
```

## Create a working sample app with Maestro tests

### Install Maestro

[Maestro install instructions](https://maestro.mobile.dev/getting-started/installing-maestro)

### Create a sample app

Follow the _Expo Go Quickstart_ instructions on [react native environment setup](https://reactnative.dev/docs/environment-setup)

Replace the contents of App.js with:

```javascript
import React, { useState } from 'react';
import { SafeAreaView, Button, Text, TextInput, StyleSheet } from 'react-native';

export default function App() {
  const [taps, setTaps] = useState(0);
  const [text, setText] = useState('')
  return (
    <SafeAreaView>
      <Button
        title="Add one"
        variant="primary"
        onPress={() => setTaps(taps + 1)}
      />
      <Button
        title="Add ten"
        testID="add_ten"
        onPress={() => setTaps(taps + 10)}
      />
      <Text>Number of taps: {taps}</Text>
      <TextInput
        testId="text_input"
        placeholder="Change me!"
        onChangeText={setText}
      />
      <Text>You typed: {text}</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

Create a test definition file called `flow.yaml`

Add the following contents:

```yaml
appId: host.exp.Exponent
---
- launchApp
- tapOn: "Add one"
- tapOn:
    id: "add_ten"
- assertVisible: "Number of taps: 11"
- tapOn: "Change me!"
- inputText: "Hello, Maestro!"
- assertVisible: "You typed: Hello, Maestro!"
```

### Start the app and test using Maestro

Run `npm start` in the react native app source directory

Select either Android or iOS Simulator

In another terminal, run `maestro test flow.yaml`

When the Expo app launches, select the app that you’re testing

### Demo

{% file src="../.gitbook/assets/Screen Recording 2023-01-11 at 21.24.32.mov" %}
React Native app tested using Maestro
{% endfile %}

## Interacting with nested components on iOS

In some cases, you may run into issues with nested tappable / accessible elements on iOS. You can resolve these issues by enabling accessibility for the inner component and disabling it for the outer container.

#### Example: Tapping on nested Text Component

```javascript
<TouchableOpacity 
  style={{ borderWidth: 1, margin: 5, padding: 10, backgroundColor: '#ddd' }} 
   accessible={false}>
  <Text>This is the wrapper button </Text>
  <TouchableOpacity 
    style={{ backgroundColor: 'red', padding: 5, width: '50%', marginTop: 10 }} 
     accessible={true}>
    <Text>I'm a small button</Text>
  </TouchableOpacity>
</TouchableOpacity>
```

&#x20;The following command will tap on the nested Text Component:

```yaml
- tapOn: "I'm a small button"
```

## Resources

* [A great introduction to Maestro with React Native](https://dev.to/b42/test-your-react-native-app-with-maestro-5bfj) by Alexander Hodes

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}
