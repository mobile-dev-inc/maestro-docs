# App Lifecycle

### launchApp

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
```

By default, the app is launched with all the permissions granted so that you don't need to handle permission dialogs.&#x20;

{% content-ref url="../app-files.md" %}
[app-files.md](../app-files.md)
{% endcontent-ref %}

### stopApp

Stops current application if it is running:

```yaml
- stopApp
```

You can also specify app id of the app to be stopped:

```yaml
- stopApp: appId
```
