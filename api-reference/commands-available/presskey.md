# pressKey

The `pressKey` command simulates pressing a physical or virtual key on a device.

### Syntax

To use the `pressKey` command, you need to define the key to be used:

```yaml
- pressKey: "keyToPress"
```

### Supported keys

The `pressKey` command accepts the following key names as arguments. You can use only one key at a time.

| Key                             | Description                                                   |
| ------------------------------- | ------------------------------------------------------------- |
| `home`                          | Simulates pressing the home button.                           |
| `lock`                          | Simulates pressing the lock button to lock the device screen. |
| `enter`                         | Simulates pressing the enter button.                          |
| `backspace`                     | Simulates pressing the backspace button.                      |
| `volume up`                     | Increases the device volume.                                  |
| `volume down`                   | Decreases the device volume.                                  |
| `back`                          | Simulates pressing the back button. Android only.             |
| `power`                         | Simulates pressing the power button. Android only.            |
| `tab`                           | Simulates pressing the tab button. Android only.              |
| `Remote Dpad Up`                | Android TV remote control key.                                |
| `Remote Dpad Down`              | Android TV remote control key.                                |
| `Remote Dpad Left`              | Android TV remote control key.                                |
| `Remote Dpad Right`             | Android TV remote control key.                                |
| `Remote Dpad Center`            | Android TV remote control key.                                |
| `Remote Media Play Pause`       | Android TV remote control key.                                |
| `Remote Media Stop`             | Android TV remote control key.                                |
| `Remote Media Next`             | Android TV remote control key.                                |
| `Remote Media Previous`         | Android TV remote control key.                                |
| `Remote Media Rewind`           | Android TV remote control key.                                |
| `Remote Media Fast Forward`     | Android TV remote control key.                                |
| `Remote System Navigation Up`   | Android TV remote control key.                                |
| `Remote System Navigation Down` | Android TV remote control key.                                |
| `Remote Button A`               | Android TV remote control key.                                |
| `Remote Button B`               | Android TV remote control key.                                |
| `Remote Menu`                   | Android TV remote control key.                                |
| `TV Input`                      | Android TV remote control key.                                |
| `TV Input HDMI 1`               | Android TV remote control key.                                |
| `TV Input HDMI 2`               | Android TV remote control key.                                |
| `TV Input HDMI 3`               | Android TV remote control key.                                |

