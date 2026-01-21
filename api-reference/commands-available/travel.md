# travel

The `travel` command mocks the motion of a user along a specified path at a given speed.

{% hint style="info" %}
The `travel` command works normally for Web tests.
{% endhint %}

### Parameters

When using the `travel` command, you need to inform the following parameter:

| Parameter | Type               | Description                                                                                                                        |
| --------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| `points`  | `list` of `string` | A set of latitude and longitude coordinates that define the path for the mocked user motion. Each coordinate is a `lat,long` pair. |
| `speed`   | `integer`          | The speed of travel in meters per second.                                                                                          |

### Usage examples

This example simulates a user traveling along a square path at orbital velocity (7.9 km/s).

```yaml
- travel:
    points:
      - "0.0,0.0"
      - "0.1,0.0"
      - "0.1,0.1"
      - "0.0,0.1"
    speed: 7900
```
