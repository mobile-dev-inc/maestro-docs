---
description: Stop a running app without clearing its data or state.
---

# stopApp

Stops a running application. The `stopApp` command can stop either the currently running application or a specific application identified by its `appId`.

### Syntax

To stop the current application, use `stopApp` with no arguments:

```yaml
- stopApp
```

If you need to stop a different application, pass an `appId`:

```yaml
-- stopApp: com.mycompany.example
```
