---
description: A step by step guide to installing Maestro on Windows
---

# Windows

{% stepper %}
{% step %}
### Download the latest Maestro Release

{% embed url="https://github.com/mobile-dev-inc/maestro/releases/latest/download/maestro.zip" %}
{% endstep %}

{% step %}
### Extract the Maestro zip

Extract the zip file you downloaded in the previous step to any location. For instance:

```
C:\Users\jake\maestro
```
{% endstep %}

{% step %}
### Update your PATH environment variable

Update your PATH environment variable to include the `maestro\bin` folder.

```
setx PATH "%PATH%;C:\Users\jake\maestro\bin"
```
{% endstep %}

{% step %}
### Connect to a device

`maestro test` will automatically detect and use any local emulator or USB-connected physical device.
{% endstep %}
{% endstepper %}
