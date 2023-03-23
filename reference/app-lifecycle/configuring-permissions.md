# Configuring Permissions

It is possible to launch an app with customized permissions behavior with maestro and change the default behavior of all permissions being granted.

You can provide permission names along with permission values to change the permission state.

### Permission Values

Permissions values can be either of the three states: `allow`, `deny` or `unset.`

| Permission Value | iOS                                                      | Android            |
| ---------------- | -------------------------------------------------------- | ------------------ |
| allow            | Permission granted                                       | Permission granted |
| deny             | Permission denied                                        | Permission denied  |
| unset            | Permission will be asked during the flow run when needed | Permission denied  |

### Permission Names

Permission names represent all the set of permissions that can be configured on a platform. For example: `bluetooth` on android supports both: `android.permission.BLUETOOTH_CONNECT` and `android.permission.BLUETOOTH_SCAN` permissions.

| Permission Names | iOS                  | Android              |
| ---------------- | -------------------- | -------------------- |
| calendar         | :white\_check\_mark: | :white\_check\_mark: |
| camera           | :white\_check\_mark: | :white\_check\_mark: |
| contacts         | :white\_check\_mark: | :white\_check\_mark: |
| health           | :white\_check\_mark: | ❌                    |
| homekit          | :white\_check\_mark: | ❌                    |
| location         | :white\_check\_mark: | :white\_check\_mark: |
| medialibrary     | :white\_check\_mark: | :white\_check\_mark: |
| microphone       | :white\_check\_mark: | :white\_check\_mark: |
| motion           | :white\_check\_mark: | ❌                    |
| notifications    | :white\_check\_mark: | :white\_check\_mark: |
| photos           | :white\_check\_mark: | ❌                    |
| reminders        | :white\_check\_mark: | ❌                    |
| siri             | :white\_check\_mark: | ❌                    |
| speech           | :white\_check\_mark: | ❌                    |
| usertracking     | :white\_check\_mark: | ❌                    |
| bluetooth        | ❌                    | :white\_check\_mark: |
| phone            | ❌                    | :white\_check\_mark: |
| storage          | ❌                    | :white\_check\_mark: |

**Note**: You can also use `all` to represent all the set of permissions that the app can ask for.

#### Supporting permission IDs for Android

There are a lot of permissions supported on Android and you might not find a few in the table above. Hence, we support permissions by directly using their IDs. For example, permission to add voice mail in the system can also be done by using the following:&#x20;

`com.android.voicemail.permission.ADD_VOICEMAIL`.

### Examples

You can mention the names and values of the permissions with `launchApp` command as follows:

#### To deny all the permissions

```yaml
- launchApp:
    permissions: { all: deny } 
```

#### To deny all the permissions but allow medialibrary

```yaml
- launchApp:
    permissions: { all: deny, medialibrary: allow } 
```

#### To deny all the permissions but allow adding voicemail

```yaml
- launchApp:
    permissions: { all: deny, com.android.voicemail.permission.ADD_VOICEMAIL: allow } 
```
