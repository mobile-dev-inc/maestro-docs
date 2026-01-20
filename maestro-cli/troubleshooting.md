# Troubleshooting

When attempting to bind the Android Debug Bridge (ADB) server to all interfaces using `adb -a -P 5037 nodaemon server`, you may encounter `smart_sockets` binding errors. This typically indicates a port conflict or an existing daemon instance. Follow these steps to reset the environment and establish a stable bridge.

## Host environment cleanup (Windows)

Before re-initializing the Android Debug Bridge server, ensure the 5037 port is vacant and the environment is isolated.

1. **Stop existing daemons:** Open Task Manager and stop all `adb.exe` processes. Alternatively, use PowerShell:

```powershell
stop-process -name adb -force

```

2. **Resource management:** Close **Android Studio** to prevent it from automatically restarting the Android Debug Bridge server with default parameters. Ensure only the **Android Emulator** remains active.
3. **Status interpretation:** If `adb devices` reports the emulator as `offline`, continue with the configuration; this state often resolves once the socket bridge initializes.

## Network and firewall configuration

WSL2 operates on a virtualized network interface. For the WSL2 client to communicate with the Windows Android Debug Bridge server, the host firewall must permit inbound traffic on the specific port.

* **Inbound Rule:** Create a Windows Defender Firewall rule to allow TCP traffic on port **5037**.
* **Corporate policy:** If you're on a managed machine, make sure your system administrator hasn't implemented policies blocking local network socket binding.

## Initializing the global Android Debug Bridge daemon

Run the following command in a persistent PowerShell terminal. **Don't close this window**, as the `nodaemon` flag keeps the process running in the foreground for logging:

```powershell
adb -a -P 5037 nodaemon server

```

## WSL2 client configuration

Now, configure your WSL2 instance to route its Android Debug Bridge traffic to the Windows host's IP address instead of its own localhost.

1. **Kill local daemon:**

```bash
adb kill-server

```

2. **Export environment variable:** Point the Android Debug Bridge client to the host's IPv4 address.

```bash
export ADB_SERVER_SOCKET=tcp:<WINDOWS_IPV4_ADDR>:5037

```

3. **Verify linkage:**

```bash
adb devices
```

The output should now list the emulator instance running on the Windows host.

## Maestro integration note

Maestro relies on a valid connection to the Android Debug Bridge server to orchestrate UI tests. If the emulator isn't fully initialized and the Windows Android Debug Bridge daemon doesn't recognize it before the Maestro flow triggers, the connection fails. Always make sure `adb devices` returns the device ID in WSL2 before running Maestro commands.
