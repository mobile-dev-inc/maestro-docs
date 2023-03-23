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
