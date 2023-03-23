# Writing Your First Flow

Write a test in a YAML file

```yaml
# flow.yaml

appId: your.app.id
---
- launchApp
- tapOn: "Text on the screen"
```

Make sure an Android device/emulator or iOS simulator is running ([instructions](installing-maestro/#android)) and app is correctly installed on a selected device ([instructions](build-and-install-your-app/)).

Run it!

```
maestro test flow.yaml
```
