# Configure Permissions

By default, all permissions are set to `allow` by the launchApp command. It is
possible to launch an app with custom permissions behaviour by passing the
`permissions` argument to `launchApp`:

```yaml
- launchApp:
    permissions:
      all: deny
      camera: allow
      location: allow
```


## Available permissions

Maestro has standardized names for most permissions.

For example, on Android: `bluetooth` targets both `android.permission.BLUETOOTH_CONNECT` and `android.permission.BLUETOOTH_SCAN`.

| Permission           | iOS support | Android support |
|----------------------|-------------|-----------------|
| calendar             | ✅          | ✅              |
| camera               | ✅          | ✅              |
| contacts             | ✅          | ✅              |
| health               | ❌          | ❌              |
| homekit              | ✅          | ❌              |
| location             | ✅          | ✅              |
| medialibrary         | ✅          | ✅              |
| microphone           | ✅          | ✅              |
| motion               | ✅          | ❌              |
| notifications        | ✅          | ✅              |
| photos               | ✅          | ❌              |
| reminders            | ✅          | ❌              |
| siri                 | ✅          | ❌              |
| speech               | ✅          | ❌              |
| usertracking         | ✅          | ❌              |
| bluetooth            | ❌          | ✅              |
| phone                | ❌          | ✅              |
| storage              | ❌          | ✅              |
| sms                  | ❌          | ✅              |
| my.custom.permission | ❌          | ✅              |

{% hint style="info" %}
Use `all` as a permission name to represent all the permissions that the app can ask for.
{% endhint %}

### Supporting permission IDs for Android

There are permissions on Android that are not listed in the table above. Use the
permission IDs in place of the permission name to set these permissions.

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
