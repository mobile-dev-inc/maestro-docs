---
description: >-
  Configure iOS and Android app permissions in Maestro tests, including camera,
  location, and other services.
---

# Configuring Permissions

Not all applications require permissions to operate, but modern mobile operating systems have a system of permissions to prevent downloaded apps from unauthorised access to system resources. This can prove challenging for test automation, since apps will prompt on the first use of that permissions, but not on subsequent uses, making the user journey inconsistent between runs of the test flow. To tackle this, Maestro allows for configuring permissions explicitly ahead of execution, making those prompts expected or avoidable.

## Permissions Setup on launch

By default, all permissions are set to `allow` by the launchApp command. It is possible to launch an app with custom permissions behaviour by passing the `permissions` argument to `launchApp`:

```yaml
- launchApp:
    permissions:
      all: deny
      camera: allow
      location: allow
```

{% content-ref url="../api-reference/commands/launchapp.md" %}
[launchapp.md](../api-reference/commands/launchapp.md)
{% endcontent-ref %}

## Setting permissions any other time

It can be useful to allow permission configuration outside of launch time, e.g. in advance of testing a deeplink or universal link, where `launchApp` isn't invoked. For this, there's `setPermissions`.

```yaml
- setPermissions:
    permissions:
      all: allow
```

{% content-ref url="../api-reference/commands/setPermissions.md" %}
[setPermissions.md](../api-reference/commands/setPermissions.md)
{% endcontent-ref %}

## Available permissions

Maestro has standardized names for most permissions.

For example, on Android: `bluetooth` targets both `android.permission.BLUETOOTH_CONNECT` and `android.permission.BLUETOOTH_SCAN`.

| Permission           | iOS support | Android support |
| -------------------- | ----------- | --------------- |
| calendar             | ✅           | ✅               |
| camera               | ✅           | ✅               |
| contacts             | ✅           | ✅               |
| health               | ❌           | ❌               |
| homekit              | ✅           | ❌               |
| location             | ✅           | ✅               |
| medialibrary         | ✅           | ✅               |
| microphone           | ✅           | ✅               |
| motion               | ✅           | ❌               |
| notifications        | ✅           | ✅               |
| photos               | ✅           | ❌               |
| reminders            | ✅           | ❌               |
| siri                 | ✅           | ❌               |
| speech               | ✅           | ❌               |
| usertracking         | ✅           | ❌               |
| bluetooth            | ❌           | ✅               |
| phone                | ❌           | ✅               |
| storage              | ❌           | ✅               |
| sms                  | ❌           | ✅               |
| my.custom.permission | ❌           | ✅               |

{% hint style="info" %}
Use `all` as a permission name to represent all the permissions that the app can ask for.
{% endhint %}

### Supporting permission IDs for Android

There are permissions on Android that are not listed in the table above. Use the permission IDs in place of the permission name to set these permissions.

For example, to allow the "add voicemail" permission, use:

```yaml
- launchApp:
    permissions:
        com.android.voicemail.permission.ADD_VOICEMAIL: allow
```

## Available permission names

Every permission can be set to: `allow`, `deny` or `unset`

| Permission Value | iOS                                      | Android                                  |
| ---------------- | ---------------------------------------- | ---------------------------------------- |
| allow            | Permission granted                       | Permission granted                       |
| deny             | Permission denied                        | Permission will be asked during flow run |
| unset            | Permission will be asked during flow run | Permission will be asked during flow run |

{% hint style="info" %}
The `allow` behavior for push notifications on iOS differs from other permissions. On iOS, the permission will _not_ be granted by default. Instead, when the permission is requested, an OS prompt will be shown, and Maestro will dismiss that prompt automatically by allowing the permission. On Android, the permission _will_ be granted by default, no OS prompt will appear.
{% endhint %}

Some iOS permissions can have other values:

| Permission | Value   | Description                              |
| ---------- | ------- | ---------------------------------------- |
| location   | always  | Same as allow                            |
|            | inuse   | Only allow location whilst using the app |
|            | never   | Same as deny                             |
| photos     | limited | Allow limited access to photos           |

## Examples

Permissions are set by passing them to the `launchApp` command as follows:

### Deny all permissions

```yaml
- launchApp:
    permissions: { all: deny } 
```

### Deny all permissions but allow the `medialibrary` permission

```yaml
- launchApp:
    permissions:
        all: deny
        medialibrary: allow
```

### Deny all permissions but allow adding voicemails

```yaml
- launchApp:
    permissions:
        all: deny
        com.android.voicemail.permission.ADD_VOICEMAIL: allow
```
