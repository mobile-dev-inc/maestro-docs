---
description: Stop a running app without clearing its data or state.
---

# stopApp

Stops a running application. The `stopApp` command can stop either the app under test or a specific application identified by its `appId`.

### Syntax

To stop the app under test, use `stopApp` with no arguments:

```yaml
- stopApp
```

If you need to stop a different application, pass an `appId`:

```yaml
- stopApp: com.mycompany.example
```
