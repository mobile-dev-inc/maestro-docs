---
description: Set permissions for an installed application.
---

# setPermissions

Used for configuring permissions of an application. This is done by default by launchApp, but might be useful at other times in the flow (e.g. before a deeplink).

To set all permissions for the app under test:

```yaml
- setPermissions:
    permissions:
      all: allow
```

To set select permissions for a different app:

```yaml
- setPermissions:
    appId: com.example.app
    permissions:
      camera: allow
      notifications: deny
```

You can read more about configuring permissions [here](../../advanced/configuring-permissions.md).

{% content-ref url="../../advanced/configuring-permissions.md" %}
[configuring-permissions.md](../../advanced/configuring-permissions.md)
{% endcontent-ref %}