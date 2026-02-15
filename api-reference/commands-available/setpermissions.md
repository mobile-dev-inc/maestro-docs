---
description: Grant or deny app permissions during flow execution.
---

# setPermissions

The `setPermissions` command configures permissions for an application. While the `launchApp` command performs this action by default, you can use `setPermissions` at other points in a flow, such as before a deeplink.

{% hint style="info" %}
`setPermissions` is available on Android and iOS.

Maestro has no control over Chrome’s permissions.
{% endhint %}

### Parameters

| Parameter     | Description                                                                                                                                                    |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `permissions` | A map of permissions to set. The key is the permission name, and the value is either `allow` or `deny`. Use the `all` key to apply a state to all permissions. |
| `appId`       | **(Optional)** The ID of the app to target. Defaults to the app under test.                                                                                    |

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

Learn how to use [permissions](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/permissions) on iOS and Android apps on flows.
