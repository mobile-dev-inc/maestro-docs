---
description: >-
  Configure React Native apps for Maestro testing on both Android and iOS
  platforms.
---

# React Native

Maestro provides full support for React Native applications on both Android and iOS. By operating at the accessibility layer, Maestro enables cross-platform testing with a single test suite, requiring zero instrumentation or modifications to your JavaScript/TypeScript source code.

### Technical advantages

* **Zero Library Dependencies**: You don't need to install any npm packages (like Detox or Appium drivers) inside your app. Maestro tests the final bundled binary.
* **Fast Feedback Loops**: Maestro interacts directly with the native views rendered by React Native, providing faster execution than traditional bridge-based testing tools.
* **Expo and EAS Ready**: Full compatibility with Expo Go, development builds, and EAS Workflows for CI/CD integration.

### Element interaction strategies

In React Native, you can target components using visible text or unique identifiers.

#### **Interacting by Text**

Maestro can interact with any component that displays text content, such as `Button` titles or `Text` components.

If you have a `Go` button, for example:

```javascript
<Button
  title="Go"
  onPress={() => Alert.alert('Success!')}
/>
```

You can create a test instruction using that element text:

```yaml
- tapOn: "Go"
```

#### **Interacting by testID**

Using visible text is easy but brittle, tests break if you change the label or translate the app. The best practice is to use the `testID` property, which Maestro maps to a unique `id`.

If you assign a `testID` to any component (Button, View, TextInput, etc.), such as in the example:

```javascript
<TextInput
  placeholder="Username"
  testID="username_input"
/>
```

When creating the test, you can target the identifier directly. This remains stable even if the placeholder or language changes.

```yaml
- tapOn:
    id: "username_input"
- inputText: "maestro_user"
```

### Platform-specific tips

#### **Expo Go vs. Standalone Builds**

When testing with Expo Go, you cannot use `launchApp` with a custom `appId` because your app runs inside the Expo container. Instead, use the `openLink` command with your development URL.

```yaml
# For Expo Go development
- openLink: exp://127.0.0.1:19000
```

For EAS builds or standalone apps, use the standard `launchApp` with your Bundle ID or Package Name.

#### **Handling nested components (iOS)**

On iOS, React Native sometimes "swallows" touch events if components are deeply nested. If you can't tap an inner element, you can resolve these issues by enabling accessibility for the inner component and disabling it for the outer container.

Consider the following example where you need to tap on the nested text component. The `accessible`  for the outer element was disabled and enabled for the inner element.

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

This way, you can target the inner element using the following command to tap on the Text component.

```yaml
- tapOn: "I'm a small button"
```

### Next Steps

If you don't know how to create tests with Maestro, access the [Quickstart](https://mobile-dev-1.gitbook.io/docs-vnext/get-started/quickstart) guide to get up and running in minutes.

To learn how to create tests, refer to the [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) documentation. If you want to explore Maestro solutions, consult the appropriate documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)
