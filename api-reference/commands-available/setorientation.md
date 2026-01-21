# setOrientation

Sets the orientation of the virtual device.

{% hint style="info" %}
If you use this command to test web applications, the command will pass, but nothing will happen.
{% endhint %}

### Arguments

The command accepts one of the following string arguments.

| Argument          | Description                                                                      |
| ----------------- | -------------------------------------------------------------------------------- |
| `PORTRAIT`        | The device is in an upright, vertical orientation. **Default**.                  |
| `LANDSCAPE_LEFT`  | The device is in a horizontal orientation, rotated 90 degrees counter-clockwise. |
| `LANDSCAPE_RIGHT` | The device is in a horizontal orientation, rotated 90 degrees clockwise.         |
| `UPSIDE_DOWN`     | The device is in an inverted, vertical orientation.                              |

### Usage examples

The following example sets the device orientation to landscape left.

```yaml
- setOrientation: LANDSCAPE_LEFT
```
