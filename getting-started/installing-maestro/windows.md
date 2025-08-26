---
description: A step by step guide to installing Maestro on Windows
---

# Windows

{% hint style="info" %}
**Prerequisites:** Maestro requires **Java 17 or higher**. You can verify your Java version with `java -version`.
{% endhint %}

## Option 1: Installation on Windows

{% stepper %}
{% step %}

#### Download the latest Maestro Release

{% embed url="https://github.com/mobile-dev-inc/maestro/releases/latest/download/maestro.zip" %}
{% endstep %}

{% step %}

#### Extract the Maestro zip

Extract the zip file you downloaded in the previous step to any location. For instance:

```shell
C:\Users\jake\maestro
```

{% endstep %}

{% step %}

#### Update your PATH environment variable

Update your PATH environment variable to include the `maestro\bin` folder. You may need to restart your terminal for this to take effect.

```
setx PATH "%PATH%;C:\Users\jake\maestro\bin"
```

{% endstep %}

{% step %}

#### Connect to a device

`maestro test` will automatically detect and use any local emulator or USB-connected physical device.
{% endstep %}
{% endstepper %}

## Option 2: Installation in WSL2

If you prefer WSL2 for your working environment, this section will walk you through the end-to-end steps for getting started with Maestro on a Windows machine.&#x20;

Note: It's more involved than installing Maestro on Windows directly, and requires passing additional configuration at runtime too.

### Pre-Requisites

1. PowerShell is installed in your Windows system.
2. Install Android Studio on your Windows machine.
3. Add ANDROID_HOME to your Windows environment variable.
   1. To check if your ANDROID_HOME setup is correctly done, open a PowerShell terminal and run this command `adb --version.`
   2. Note down the ADB version.
4. Install Java JDK 17 or higher and set JAVA_HOME
   1. Run `java -version` to check if Java 17+ is installed correctly.

### Steps

1. Install WSL2 (Window Subsystem for Linux)
2. Install Java 17 or higher
3. Install Maestro

#### 1. Install WSL 2

With recent Windows 11, Microsoft has made it pretty easy to install Windows Subsystem for Linux, aka WSL.

In order to install WSL, open PowerShell as administrator and run the following command:

```bash
wsl --install
```

After running the above command, follow through instructions and restart the computer.

Install [Windows Terminal](https://github.com/microsoft/terminal) application for refreshing terminal experience.

Set your Linux username and password (Something that you will not forget).

Run the following two commands to update your Ubuntu system. Enter password when prompted.

```bash
sudo apt update
sudo apt upgrade
```

#### 2. Install Java

After restarting the system, open the Terminal application and click on the dropdown to select Ubuntu. Install Java 17 or higher with the following command:

```bash
sudo apt install openjdk-17-jdk
```

Alternatively, you can install a newer version like Java 21:

```bash
sudo apt install openjdk-21-jdk
```

#### 3. Install Maestro

Installing Maestro is now just a matter of running following one command.

```shell
     curl -Ls "https://get.maestro.mobile.dev" | bash
```

**Tada! 🎉**

**You have successfully installed Maestro on your Windows machine** 🙌

Check your Maestro version using the following command:

```bash
maestro --version
```

### What's Next?

#### Let's set you up to use Android in your freshly installed WSL2

- Download the Android command line tools zip file from [Android official site.](https://developer.android.com/studio)
- Use the following instructions to set up Android command lines correctly in your WSL2.

  - Open WSL2 terminal.
  - Create a new directory in your home directory.

    ```shell
    ~ $ mkdir Android
    ~ $ cd Android
    ```

  - Unzip the Android command line tools zip file in the `android` directory using this command: `unzip ~<command_line_zip_filename>.zip`
  - In the `Android` directory perform following actions.

    ```shell
    $ mkdir latest
    $ mv cmdline-tools/* latest/
    $ mv latest/ cmdline-tools/
    ```

    **Note:** Last command will probably give you a warning, but you don’t need the worry about that.

  - Now add the following line to your `~/.bashrc file`

    ```shell
    export ANDROID_HOME=$HOME/Android
    export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
    ```

  - Save your `~/.bashrc` file and exit.
  - Run `source ~/.bashrc` to reload the bashrc file.
  - Now, we will install basic Android utilities using the following commands:
    - Run `sdkmanager --list` to check if everything is working fine.
    - Run `sdkmanager --install "platform-tools"` to install platform tools.
  - Finally, add the following into your `~/.bashrc` file
    - `export PATH=$PATH:$ANDROID_HOME/platform-tools`
    - Save your `~/.bashrc` file and exit.
    - Run `source ~/.bashrc` to reload the bashrc file.
  - To check that everything went well, do the following:
    - Close and relaunch terminal
    - Run `adb --version` and see that adb version is shown
    - Since everything is installed fresh, your WSL 2 adb version should perfectly match with Windows ADB version that we noted down as part of the pre-requisites.

Please follow the below steps to setup the ADB and make sure you are able to use Android emulators with your WSL2 correctly:

- Launch your Android emulator on Windows.
- Once the Android emulator is up and running, open a PowerShell prompt.
- Run this command in PowerShell

  ```powershell
  adb -a -P 5037 nodaemon server
  ```

- This will start the adb server in the Windows host.
- Note down the IPV4 address of your Windows host PC/machine.

TROUBLESHOOTING:

- Sometimes you may get `smartsockets..` error when you run `adb -a -P 5037 nodaemon server` command in PowerShell. In that case, you can do the following steps:
  - Open task manager and kill all `adb` related processes.
  - If Android Studio is open, close it and **keep only** emulator running.
  - If you see a message saying `emulator offline`, **ignore it**.
  - Sometimes, the firewall stops your connection with the host machine. For that, add a firewall rule to allow the connection or check with your organization system admin if using a company machine.
- **Note: Don't close the PowerShell terminal!**
- Now open your WSL2 terminal and run these commands:
  - `adb kill-server`
  - `export ADB_SERVER_SOCKET=tcp:<WINDOWS_IPV4_ADDR>:5037`
  - `adb devices`
  - `You should see your connected emulator successfully now.`

#### Ready to start Using Maestro?

Yes, at this point, you are free to start your automation.

- [Write your first flow](https://docs.maestro.dev/getting-started/writing-your-first-flow)
- How to run **Maestro commands**?
  - You can run Maestro commands in WSL2 terminal with `--host` flag. eg.
    - _**maestro --host \<WINDOWS_IPV4_ADDR> test flow.yaml**_
    - _**maestro --host \<WINDOWS_IPV4_ADDR> studio**_
- Check out the [full documentation](https://docs.maestro.dev/)

### Known Issues

- If your Android emulator is not up and running in the Windows host, the Maestro test command fails to find the installed emulator. At this point, it is recommended that you fire up your emulator before running the flow using Maestro.
