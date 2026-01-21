# stopApp

Stops a running application. The `stopApp` command can stop either the currently running application or a specific application identified by its `appId`.

### Syntax

To stop the current application, you need to use the `stopApp` with no arguments:

```yaml
- stopApp
```

If you need to stop a specific application, you need to inform the `appId`:&#x20;

```yaml
- stopApp: my-app-id
```
