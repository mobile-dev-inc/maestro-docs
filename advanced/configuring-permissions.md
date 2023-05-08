# Configuring Permissions

By default, all permissions are set to `allow` by the launchApp command. It is possible to launch an app with custom permissions behaviour by passing the `permissions` argument to `launchApp`.

### Permission Name

Maestro has standardised names for most permissions.

For example, on Android: `bluetooth` targets both `android.permission.BLUETOOTH_CONNECT` and `android.permission.BLUETOOTH_SCAN`.

| Permission           | iOS support          | Android support      |
| -------------------- | -------------------- | -------------------- |
| calendar             | :white\_check\_mark: | :white\_check\_mark: |
| camera               | :white\_check\_mark: | :white\_check\_mark: |
| contacts             | :white\_check\_mark: | :white\_check\_mark: |
| health               | ❌                    | ❌                    |
| homekit              | :white\_check\_mark: | ❌                    |
| location             | :white\_check\_mark: | :white\_check\_mark: |
| medialibrary         | :white\_check\_mark: | :white\_check\_mark: |
| microphone           | :white\_check\_mark: | :white\_check\_mark: |
| motion               | :white\_check\_mark: | ❌                    |
| notifications        | :white\_check\_mark: | :white\_check\_mark: |
| photos               | :white\_check\_mark: | ❌                    |
| reminders            | :white\_check\_mark: | ❌                    |
| siri                 | :white\_check\_mark: | ❌                    |
| speech               | :white\_check\_mark: | ❌                    |
| usertracking         | :white\_check\_mark: | ❌                    |
| bluetooth            | ❌                    | :white\_check\_mark: |
| phone                | ❌                    | :white\_check\_mark: |
| storage              | ❌                    | :white\_check\_mark: |
| sms                  | ❌                    | :white\_check\_mark: |
| my.custom.permission | ❌                    | :white\_check\_mark: |

**Note**: Use `all` as a permission name to represent all the permissions that the app can ask for.

#### Supporting permission IDs for Android

There are permissions on Android that are not listed in the table above. Use the permission IDs in place of the permission name to set these permissions.

For example, to allow the "add voicemail" permission, use:

```yaml
- launchApp:
    permissions:
        com.android.voicemail.permission.ADD_VOICEMAIL: allow
```

### Permission Value

Every permission can be set to: `allow`, `deny` or `unset`

| Permission Value | iOS                                      | Android                                  |
| ---------------- | ---------------------------------------- | ---------------------------------------- |
| allow            | Permission granted                       | Permission granted                       |
| deny             | Permission denied                        | Permission will be asked during flow run |
| unset            | Permission will be asked during flow run | Permission will be asked during flow run |

Some iOS permissions can have other values

| Permission | Value   | Description                              |
| ---------- | ------- | ---------------------------------------- |
| location   | always  | Same as allow                            |
|            | inuse   | Only allow location whilst using the app |
|            | never   | Same as deny                             |
| photos     | limited | Allow limited access to photos           |

### Examples

Permissions are set by passing them to the `launchApp` command as follows:

#### Deny all permissions

```yaml
- launchApp:
    permissions: { all: deny } 
```

#### Deny all permissions but allow the medialibrary permission

```yaml
- launchApp:
    permissions:
        all: deny
        medialibrary: allow
```

#### Deny all permissions but allow adding voicemails

```yaml
- launchApp:
    permissions:
        all: deny
        com.android.voicemail.permission.ADD_VOICEMAIL: allow
```
