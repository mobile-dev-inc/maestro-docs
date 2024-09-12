# killApp

The `killApp` command kills the App on Android but is just an alias for `stopApp` on iOS and Web.

```yaml
- killApp
```
By killing the app on Android, you can trigger **System-initiated Process Death**. It is the equivalent of: 
```bash
adb shell am kill {package name}
```
Here is an example how to fully reproduce System-initiated Process Death:
```yaml
appId: com.example
---
- pressKey: Home # Puts the app into the background
- killApp # Kills the app (adb shell am kill)
- launchApp: # Relaunches the app
    stopApp: false # Without adb shell am stop
```

It is advised to use this set of commands as a subFlow (ex: `trigger-process-death.yaml`) and re-use it via `runFlow` in every other test, to re-check the data of the screen under test after **System-initiated Process Death**:

```yaml
appId: com.example
---
- launchApp
- tapOn:
    id: "com.example:id/enter_name"
- inputText: "John Doe"
- tapOn:
    id: "com.example:id/next"
- assertVisible:
    id: "com.example:id/show_name"
    text: "Name = John Doe"
    enabled: true
- runFlow: trigger-process-death.yaml
- assertVisible:
    id: "com.example:id/show_name"
    text: "Name = John Doe"
    label: "Asserts that \"Name = John Doe\" meaning the screen kept its data after System-initiated Process Death"
    enabled: true
- stopApp
```
