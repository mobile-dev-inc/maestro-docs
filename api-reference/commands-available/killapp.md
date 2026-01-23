# killApp

The `killApp` command terminates the running application.

{% hint style="info" %}
The `killApp` has no effect over Web tests.
{% endhint %}

{% hint style="info" %}
#### Android&#x20;

On Android, this command triggers a system-initiated process death, which is equivalent to running `adb shell am kill {package name}`.&#x20;
{% endhint %}

### Syntax

The command takes no arguments.

```yaml
- killApp
```

### Usage examples

The following example demonstrates how to trigger and recover from a system-initiated process death on Android. This sequence is useful for testing an application's ability to restore its state.

```yaml
# trigger-process-death.yaml
appId: com.example
---
- pressKey: Home # Puts the app into the background
- killApp # Kills the app via system-initiated process death
- launchApp: # Relaunches the app
    stopApp: false # Ensures a clean launch without an initial stop command
```

### Best practices

Maestro team recommends defining the process death commands as a reusable [subflow](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/nested-flows) (e.g., `trigger-process-death.yaml`) and calling it via `runFlow` in your tests. This ensures that the screen under test maintains its data after the system-initiated process death.

The following example demonstrates how to verify data persistence:

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

### Related commands

* [stopapp.md](stopapp.md "mention")
* [launchapp.md](launchapp.md "mention")
