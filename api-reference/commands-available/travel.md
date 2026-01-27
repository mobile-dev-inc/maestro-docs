# travel

The `travel` command mocks the motion of a user along a specified path at a given speed.

### Parameters

When using the `travel` command, you need to inform the following parameter:

| Parameter | Type               | Description                                                                                                                        |
| --------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| `points`  | `list` of `string` | A set of latitude and longitude coordinates that define the path for the mocked user motion. Each coordinate is a `lat,long` pair. |
| `speed`   | `integer`          | The speed of travel in meters per second.                                                                                          |

### Usage examples

This example simulates a user traveling along a route from Paris to Rome at 150 km/s (about 10 seconds).

```yaml
- travel:
    points:
      - "48.8578065, 2.295188"
      - "46.2276, 5.9900"
      - "43.7230, 10.3966"
      - "41.8902, 12.4922"
    speed: 150000
    speed: 7900
```
