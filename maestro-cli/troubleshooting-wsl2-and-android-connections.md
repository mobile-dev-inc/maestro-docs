---
description: >-
  Fix WSL2 and Android Emulator connectivity issues. Resolve ADB port 5037
  conflicts, configure firewall, and set ADB_SERVER_SOCKET for Windows.
---

# Troubleshooting: WSL2 and Android Connections

This page addresses connectivity issues specifically encountered when running Maestro within Windows Subsystem for Linux (WSL2) while using an Android Emulator hosted on Windows.

### The Problem

When attempting to bridge the connection between WSL2 and Windows using `adb -a -P 5037 nodaemon server`, you may encounter `smart_sockets` errors. This typically indicates that port 5037 is already in use or a background ADB process is conflicting with your setup.

{% stepper %}
{% step %}
### Host environment cleanup (Windows)&#xD;

Before re-initializing the connection, you must isolate the environment on your Windows host.

1.  Open Task Manager and end all `adb.exe` processes, or run the following in PowerShell:<br>

    ```powershell
    stop-process -name adb -force
    ```
2. Close Android Studio to prevent it from automatically restarting the ADB server with default settings. Keep the Android Emulator active.
3. If `adb devices` shows the emulator as `offline` at this stage, proceed anyway; the status usually resolves once the bridge is established.
{% endstep %}

{% step %}
### Network and firewall configuration&#xD;

WSL2 runs on a virtualized network. Your Windows firewall must be configured to allow this external traffic.

* **Inbound Rule**: Create a rule in Windows Defender Firewall to allow TCP traffic on port 5037.
* **Corporate Policies**: If using a managed work machine, ensure your administrator has not blocked local network socket binding.
{% endstep %}

{% step %}
### Initialize the global ADB daemon

Open a PowerShell terminal and run the following command. Keep this window open, as closing it will terminate the connection bridge:

```powershell
adb -a -P 5037 nodaemon server
```
{% endstep %}

{% step %}
### WSL2 client configuration&#xD;

Configure your WSL2 instance to look for the ADB server on your Windows host rather than its own local environment.

1.  Kill the local server:

    ```bash
    adb kill-server
    ```
2.  Find your Windows IPv4 address and export it to the environment:

    ```bash
    export ADB_SERVER_SOCKET=tcp:<WINDOWS_IPV4_ADDR>:5037
    ```
3.  Verify the link:

    ```bash
    adb devices
    ```

The output should now list the emulator instance running on the Windows host.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
### Maestro integration note

Maestro requires a stable ADB connection to orchestrate tests. If the Windows ADB daemon does not recognize the emulator before you start a Maestro Flow, the test will fail.

Always verify that `adb devices` returns a valid device ID in your WSL2 terminal before running Maestro commands.
{% endhint %}

### Still having issues?

If you are not using WSL2 and are seeing different errors, join the `#maestro-questions` channel in the Maestro [Slack community](https://maestrodev.typeform.com/to/FelIEe8A).
