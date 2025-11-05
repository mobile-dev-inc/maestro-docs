---
description: >-
  Set maestro_driver_startup_timeout to extend driver startup time and prevent
  failures in slow environments.
---

# Configure Maestro Driver Startup Timeout for Reliable Tests

In some environments with limited performance, such as CI/CD, it may be necessary to increase the maestro driver's default startup timeout. For this, you can set the environment `MAESTRO_DRIVER_STARTUP_TIMEOUT`, setting how many milliseconds you want.

The default value is `15000` (15 seconds)

Example

```
export MAESTRO_DRIVER_STARTUP_TIMEOUT=60000 # setting 60 seconds
maestro test file.yaml
```
