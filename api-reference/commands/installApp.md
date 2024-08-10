# installApp
The `installApp` command installs an application on a device, ensuring that the specific version of the app you want to test is correctly deployed. This command is crucial when you need to verify that a particular build or configuration of an app behaves as expected on the device.

```
- installApp: "path/to/app.apk"
```
For Android, this command performs the equivalent of running the following command in the terminal:
bash
Kodu kopyala
```
adb install "path/to/app.apk"
```

For iOS, it performs the equivalent of running the following command:

```
xcrun simctl install booted "path/to/app.ipa"
```

# Example of Using installApp
Below is an example of how to use the installApp command within a Maestro flow. In this scenario, the app is first installed, and then a series of actions are performed to verify the app's behavior:

```
appId: com.example
---
- installApp: "path/to/app.apk"
- launchApp
- tapOn:
  id: "com.example:id/start_button"
- assertVisible:
  id: "com.example:id/home_screen"
  text: "Welcome to Example App"
  enabled: true
- stopApp
```