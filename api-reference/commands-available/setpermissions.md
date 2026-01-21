# setPermissions

The `setPermissions` command configures permissions for an application. While the `launchApp` command performs this action by default, you can use `setPermissions` at other points in a flow, such as before a deeplink.

{% hint style="info" %}
`setPermissions` is available on Android and iOS.

Maestro has no control over Chrome’s permissions.
{% endhint %}

### Parameters

<table><thead><tr><th width="149">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>permissions</code></td><td> A map of permissions to set. The key is the permission name, and the value is either <code>allow</code> or <code>deny</code>. Use the <code>all</code> key to apply a state to all permissions.</td></tr><tr><td><code>appId</code></td><td><strong>(Optional)</strong> The ID of the app to target. Defaults to the app under test.</td></tr></tbody></table>

### Usage examples

The following examples demonstrate how to use the `setPermissions` command.

#### Grant all permissions

This example grants all permissions to the app under test.

```yaml
- setPermissions:
    permissions:
      all: allow
```

#### Set specific permissions for another app

This example sets the `camera` permission to `allow` and the `notifications` permission to `deny` for the app with the ID `com.example.app`.

```yaml
- setPermissions:
    appId: com.example.app
    permissions:
      camera: allow
      notifications: deny
```

### Related content

Learn how to configure the permissions by accessing the [guide](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/permissions).
