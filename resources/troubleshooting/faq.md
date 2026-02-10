---
description: Frequently asked questions about Maestro installation and usage.
---

# FAQ

Find answers to common Maestro questions: parameters, assertions, YAML gotchas, cloud behavior, and how to organize your tests.

<details>

<summary>How can I use the same flow when my apps have different app IDs?</summary>

Use an [external parameter](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants) for `appId` and pass it when you run Maestro. For example, pass `APP_ID` when testing with the Maestro CLI:

```bash
maestro test -e APP_ID=your.app.id file.yaml
```

In your Flow, refer to it with `${APP_ID}`:

```yaml
appId: ${APP_ID}
---
- launchApp
```

</details>

<details>

<summary>How do I assert on a string that contains a dollar sign?</summary>

Maestro treats `$` as the start of a variable. Escape the dollar so it is treated as literal text:

```yaml
- assertVisible: \$150 in Cash
```

</details>

<details>

<summary>How do I compare two values?</summary>

To assert on values that appear on different screens, store each value in a variable with [`copyTextFrom`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/copytextfrom) and [`evalScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/evalscript), then compare in a `runFlow` with a `when` condition:

```yaml
# Navigate to first value, then:
- copyTextFrom:
    id: 'listView1'
- evalScript: ${output.firstPrice = maestro.copiedText}

# Navigate to second value, then:
- copyTextFrom:
    id: 'detailView'
- evalScript: ${output.secondPrice = maestro.copiedText}

# Compare:
- runFlow:
    when:
      true: ${output.firstPrice === output.secondPrice}
    commands:
      - evalScript: ${console.log('Prices match! Both are ' + output.secondPrice)}
```

</details>

<details>

<summary>How do I generate a random number?</summary>

Maestro offers built-in support for random numbers, so you don't need to write external scripts.

You can use the [`inputRandomNumber`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/inputtext#random-text-input-commands) command if you need to type the number directly into a field:

```yaml
- inputRandomNumber:
    length: 8
```

Another option is to use Faker. Use this option if you need to store the number in a variable or use it within a specific range, use the built-in [`faker`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/javascript/generate-synthetic-data) library via `evalScript`:&#x20;

```yaml
- evalScript: ${output.thisNumber = faker.expression("#{number.numberBetween '1' '10'}")}
```

</details>

<details>

<summary>Why does YES get translated to true, and NO to false?</summary>

If you use `tapOn: YES` or `tapOn: NO`, Maestro may interpret them as booleans and attempt to find the text `"true"` or `"false"` instead:

```yaml
appId: com.example
---
- launchApp
- tapOn: YES
```

You may see an error like:

```bash
 ║  > Flow: flow                         
 ║                                       
 ║    ❌   Tap on "true"                 
 ║                                       
                                         
Element not found: Text matching regex: true

Element with Text matching regex: true not found. Check the UI hierarchy in debug artifacts to verify if the element exists.
```

This behavior comes from YAML itself. The [YAML specification](https://yaml.org/type/bool.html) allows booleans to be written as `true`/`false`, `yes`/`no`, `on`/`off`, or `Y`/`N` (in various casings). As a result, unquoted `YES` and `NO` are parsed as booleans.

To work around this, force the value to be treated as literal text by quoting it, or use a regular expression:

```yaml
- tapOn: "YES"
- tapOn: ^No    # Text that begins with "No"
```

</details>

<details>

<summary>Why are my tests slower in Maestro's cloud environment?</summary>

The cloud environment prioritizes reliability and repeatability: each device is wiped and recreated between tests so one run cannot affect another. While this adds about 45 seconds between tests compared with running locally, it ensures a clean state for every execution.

To reduce total run time:

* Add more parallel runners.
* Restructure tests into fewer, longer flows, without sacrificing reliability or useful failure information.

</details>

<details>

<summary>How do I connect WSL2 to the Android Simulator running on Windows?</summary>

When attempting to bridge the connection between WSL2 and Windows using `adb -a -P 5037 nodaemon server`, you may encounter `smart_sockets` errors. This typically indicates that port 5037 is already in use or a background ADB process is conflicting with your setup.

#### Host environment cleanup (Windows)&#xD;

Before re-initializing the connection, you must isolate the environment on your Windows host.

1.  Open Task Manager and end all `adb.exe` processes, or run the following in PowerShell:<br>

    ```powershell
    stop-process -name adb -force
    ```
2. Close Android Studio to prevent it from automatically restarting the ADB server with default settings. Keep the Android Emulator active.
3. If `adb devices` shows the emulator as `offline` at this stage, proceed anyway; the status usually resolves once the bridge is established.

#### Network and firewall configuration

WSL2 runs on a virtualized network. Your Windows firewall must be configured to allow this external traffic.

* **Inbound Rule**: Create a rule in Windows Defender Firewall to allow TCP traffic on port 5037.
* **Corporate Policies**: If using a managed work machine, ensure your administrator has not blocked local network socket binding.

#### Initialize the global ADB daemon

Open a PowerShell terminal and run the following command. Keep this window open, as closing it will terminate the connection bridge:

```powershell
adb -a -P 5037 nodaemon server
```

#### WSL2 client configuration&#xD;

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

{% hint style="info" %}
#### Maestro integration note

Maestro requires a stable ADB connection to orchestrate tests. If the Windows ADB daemon does not recognize the emulator before you start a Maestro Flow, the test will fail.

Always verify that `adb devices` returns a valid device ID in your WSL2 terminal before running Maestro commands.
{% endhint %}

#### Still having issues?

If you are not using WSL2 and are seeing different errors, join the `#maestro-questions` channel in the Maestro [Slack community](https://maestrodev.typeform.com/to/FelIEe8A).

#### &#xD;

</details>
