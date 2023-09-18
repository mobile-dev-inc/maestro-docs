---
description: Maestro offers a few convenience methods to start or create a device
---

# Start Device

You can use Maestro to create an Android emulator or an iOS simulator.&#x20;

The device configurations are similar to the ones hosted on Maestro Cloud. Using such devices will help you create Maestro Cloud compatible flows.



### Start an Android emulator using Maestro

You can start by running

```sh
maestro start-device --platform android
```

This will create a default Android emulator (Pixel 6, Google APIs 30). If the devices already exists, it will simply launch it.

For full options run `maestro start-device`

_Note: Device configurations are limited to a few recommended os versions and devices. Such configurations work well with Maestro and Maestro Cloud._

### Start an iOS simulator using Maestro

You can start by running

```
maestro start-device --platform ios
```

This will create a default iOS simulator (iPhone11, iOS 15.5). If the devices already exists, it will simply launch it.

For full options run `maestro start-device`

_Note: Device configurations are limited to a few recommended os versions and devices. Such configurations work well with Maestro and Maestro Cloud._

