# setLocation

`setLocation` command applies a mock geolocation to the device:

```
- setLocation:
    latitude: 52.3599976
    longitude: 4.8830301
```

{% hint style="warning" %}
Note that this does not update the _location_ of the emulator/simulator when running in Maestro Cloud so if your backend/app relies on IP location, this will still be set to the default location which is US
{% endhint %}
