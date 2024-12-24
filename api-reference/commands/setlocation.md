# setLocation

`setLocation` command applies a mock geolocation to the device:

```
- setLocation:
    latitude: 52.3599976
    longitude: 4.8830301
```

{% hint style="warning" %}
Note that this only updates the co-ordinate location of the emulator/simulator. When running in [Robin](https://www.robintest.com/), if your app relies on IP location, this will still resolve to US.
{% endhint %}

{% hint style="info" %}
Note that for Android, this only works on API level 31 or above. Support for lower levels is coming soon!
{% endhint %}
