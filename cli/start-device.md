---
description: Maestro offers a few convenience methods to start or create a device
---

# Start Device

You can use Maestro to create an Android emulator or an iOS simulator.&#x20;

The device configurations are similar to the ones hosted on [Maestro's cloud platform](../cloud/run-maestro-tests-in-the-cloud.md). Using such devices will help you create compatible flows.



### Start an Android emulator using Maestro

You can start by running

```sh
maestro start-device --platform android
```

This will create a default Android emulator (Pixel 6, Google API 30). If the device already exists, it will simply launch it.

For full options run `maestro start-device`

_Note: Device configurations are limited to a few recommended OS versions and devices. Such configurations work well when_ [_running flows in the cloud_](../cloud/run-maestro-tests-in-the-cloud.md)_._

### Start an iOS simulator using Maestro

You can start by running

```
maestro start-device --platform ios
```

This will create a default iOS simulator (iPhone11, iOS 15.5). If the device already exists, it will simply launch it.

For full options run `maestro start-device`

_Note: Device configurations are limited to a few recommended os versions and devices. Such configurations work well when_ [_running flows in the cloud_](../cloud/run-maestro-tests-in-the-cloud.md)_._

