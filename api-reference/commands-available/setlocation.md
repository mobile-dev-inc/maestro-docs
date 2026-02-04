---
description: Set device GPS location to specific coordinates for location testing.
---

# setLocation

The `setLocation` command applies a mock geolocation to the device.

### Arguments

The following arguments are available for the `setLocation` command.

<table><thead><tr><th width="121">Argument</th><th>Description</th></tr></thead><tbody><tr><td><code>latitude</code></td><td>The latitude coordinate.</td></tr><tr><td><code>longitude</code></td><td>The longitude coordinate.</td></tr></tbody></table>

### Usage examples

The following example sets the device's location to Amsterdam.

```yaml
- setLocation:
    latitude: 52.3599976
    longitude: 4.8830301
```

### Limitations

Keep the following limitations in mind when using `setLocation`:

* On Android, this command requires API level `31` or higher.
* The command only updates the device's coordinate-based location. When running tests in Maestro Cloud, services that rely on IP-based geolocation still resolve to a US-based IP address.
