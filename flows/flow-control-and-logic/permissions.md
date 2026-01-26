# Permissions

Managing system permissions is a common challenges in mobile test automation. Since OS prompts (like "Allow Camera Access") typically only appear once, your test journey can become inconsistent if the app state isn't reset.

Maestro solves this by allowing you to explicitly configure permissions either at launch or during the Flow, ensuring a predictable environment every time.

### Configure permissions on launch

The easiest way to manage permissions is during the [`launchApp`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/launchapp) command.By default, Maestro grants all permissions, but you can override this behavior to test specific scenarios.

To customize launch permissions, you need to specify them when calling `launchApp`. The following example denies all permissions but explicitly allows the camera and location:

```yaml
- launchApp:
    permissions:
      all: deny
      camera: allow
      location: allow
```

### Changing permissions mid-flow

Sometimes you need to change permissions while the app is running, for example, to test how your app handles a permission denial or to prepare for a specific feature flow like scanning a QR code. Use the [`setPermissions`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/setpermissions) command for this purpose.

```yaml
- setPermissions:
    permissions:
      notifications: allow
```

{% hint style="info" %}
#### Browser limitation

Maestro can manage permissions for iOS and Android applications, but it has no control over Chrome’s system permissions.
{% endhint %}

### Available permissions

Maestro uses standardized names to make your Flows cross-platform. For example, using `bluetooth` on Android targets both `BLUETOOTH_CONNECT` and `BLUETOOTH_SCAN` automatically.

The following table list all permissions available in iOS and Android.

| Permission      | iOS | Android |
| --------------- | --- | ------- |
| `calendar`      | ✅   | ✅       |
| `camera`        | ✅   | ✅       |
| `contacts`      | ✅   | ✅       |
| `health`        | ❌   | ❌       |
| `homekit`       | ✅   | ❌       |
| `location`      | ✅   | ✅       |
| `medialibrary`  | ✅   | ✅       |
| `microphone`    | ✅   | ✅       |
| `motion`        | ✅   | ❌       |
| `notifications` | ✅   | ✅       |
| `photos`        | ✅   | ❌       |
| `reminders`     | ✅   | ❌       |
| `siri`          | ✅   | ❌       |
| `speech`        | ✅   | ❌       |
| `usertracking`  | ✅   | ❌       |
| `bluetooth`     | ❌   | ✅       |
| `phone`         | ❌   | ✅       |
| `storage`       | ❌   | ✅       |
| `sms`           | ❌   | ✅       |

{% hint style="success" %}
To grant all available permissions, use `all: allow` to represent all the permissions that the app can request.
{% endhint %}

#### **Android custom permissions**

If a specific Android permission isn't listed above, you can use the full Android Permission ID. The following example adds the `ADD_VOICEMAIL` permission:

```yaml
- setPermissions:
    permissions:
      com.android.voicemail.permission.ADD_VOICEMAIL: allow
```

### Permission values

You can set permissions to one of the following states:

<table><thead><tr><th width="122.3333740234375">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>allow</code></td><td><p>Grants the permission. </p><p></p><p>On iOS, this also automatically dismisses the system prompt.</p></td></tr><tr><td><code>deny</code></td><td><p>Denies the permission.<br></p><p>Android will request permission during the Flow execution if the app requires access to a specific feature.</p></td></tr><tr><td><code>unset</code></td><td>Resets the permission state, causing the system to prompt permission requests when running the Flow.</td></tr></tbody></table>

{% hint style="info" %}
#### **Push notifications on iOS**

Unlike other permissions, iOS does not grant notification permissions silently. When the app requests permissions, the system prompt appears, and Maestro automatically taps **Allow**.&#x20;

On Android, the permission is granted silently without a prompt.
{% endhint %}

#### iOS-specific values

iOS supports additional granular values for certain permissions.

<table><thead><tr><th width="122.3333740234375">Permission</th><th width="98">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>location</code></td><td><code>always</code></td><td>Grants <strong>Always Allow</strong> location access.</td></tr><tr><td></td><td><code>inuse</code></td><td>Grants <strong>While Using the App</strong> location access.</td></tr><tr><td></td><td><code>never</code></td><td>Same as <code>deny</code>.</td></tr><tr><td><code>photos</code></td><td><code>limited</code></td><td>Grants <strong>Limited Access</strong> to the photo library.</td></tr></tbody></table>

### Usage examples

#### Deny all permissions

To ensure your app handles permission denied states, start your Flow by denying everything. This forces you to handle the edge cases where a user says No when the system ask their permission.

```yaml
- launchApp:
    permissions:
        all: deny
```

#### Deny all but allow specific ones

This is a common pattern for testing specific features in isolation.

```yaml
- launchApp:
    permissions:
        all: deny
        medialibrary: allow
```

#### Allow specific Android custom permission

This example enables voicemail permissions using the specific Android package name.

```yaml
- launchApp:
    permissions:
        all: deny
        com.android.voicemail.permission.ADD_VOICEMAIL: allow
```

### Related resources&#xD;

* [`launchApp`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/launchapp): See the full technical reference for launching apps.
* &#x20;[`setPermissions`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/setpermissions): Technical parameters for mid-flow configuration.
