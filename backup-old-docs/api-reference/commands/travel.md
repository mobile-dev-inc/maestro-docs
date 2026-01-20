# travel

The `travel` command can be used to mock the motion of the user, by specifying a set of points (lat/long coordinates) and a speed:

```yaml
- travel:
    points: # set of lat/long coordinates where user motion should be mocked
      - 0.0,0.0
      - 0.1,0.0
      - 0.1,0.1
      - 0.0,0.1
    speed: 7900 # 7.9 km/s aka orbital velocity
```
