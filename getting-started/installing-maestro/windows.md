---
description: A step by step guide to installing Maestro on Windows
---

# Windows

Maestro works great on Windows computers, but there are a few unique setup steps to be aware of. This guide will walk you through the end-to-end steps for getting started with Maestro on a Windows machine.

### Pre-Requisites

1. PowerShell is installed in your Windows system.
2. Install [Android Studio](https://developer.android.com/studio) on your Windows machine.
3. Add ANDROID\_HOME to your Windows environment variable.
   1. To check if your ANDROID\_HOME setup is correctly done, open a PowerShell terminal and run this command `adb --version`.
   2. Note down the ADB version.
4. Install Java JDK 11 and set JAVA\_HOME
   1. Run `java --version` to check if the Java is installed correctly.

## Steps <a href="#8b4a" id="8b4a"></a>

1. Install WSL2 (Window Subsystem for Linux)
2. Install Java 21
3. Install Maestro

## 1. Install WSL 2 <a href="#0215" id="0215"></a>

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

## 2. Install Java <a href="#5521" id="5521"></a>

After restarting the system, open the Terminal application and click on the dropdown to select Ubuntu. Type in the following command:

```bash
sudo apt install openjdk-21-jdk
```

## 3. Install Maestro

Installing Maestro is now just a matter of running following one command.

```
curl -Ls "https://get.maestro.mobile.dev" | bash
```

**Tada! 🎉**

**You have successfully installed Maestro on your Windows machine** 🙌

Check your Maestro version using the following command:

```bash
maestro --version
```

## What's Next? <a href="#7639" id="7639"></a>

### Let's set you up to use Android in your freshly installed WSL2

* Download the Android command line tools zip file from [Android official site.](https://developer.android.com/studio)
*   Use the following instructions to set up Android command lines correctly in your WSL2.

    * Open WSL2 terminal.
    * Create a new directory in your home directory.

    ```
    $ mkdir Android
    $ cd Android
    ```

    * Unzip the Android command line tools zip file in the `android` directory using this command: `unzip ~<command_line_zip_filename>.zip`
    * In the  `Android` directory perform following actions.

    ```
    $ mkdir latest
    $ mv cmdline-tools/* latest/
    $ mv latest/ cmdline-tools/
    ```

    **Note:** Last command will probably give you a warning, but you don’t need the worry about that.

    * Now add the following line to your `~/.bashrc file`

    ```
    export ANDROID_HOME=$HOME/Android
    export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
    ```

    * Save your `~/.bashrc` file and exit.
    * Run `source ~/.bashrc` to reload the bashrc file.
    * Now, we will install basic Android utilities using the following commands:
      * Run `sdkmanager --list` to check if everything is working fine.
      * Run `sdkmanager --install "platform-tools"` to install platform tools.
    * Finally, add the following into your `~/.bashrc` file
      * `export PATH=$PATH:$ANDROID_HOME/platform-tools`
      * Save your `~/.bashrc` file and exit.
      * Run `source ~/.bashrc` to reload the bashrc file.
    * To check that everything went well, do the following:
      * Close and relaunch terminal
      * Run `adb --version` and see that adb version is shown
      * Since everything is installed fresh, your WSL 2 adb version should perfectly match with Windows ADB version that we noted down as part of the pre-requisites.

**Please follow the below steps to setup the ADB and make sure you are able to use Android emulators with your WSL2 correctly**

* Fire up your Android emulator on Windows.
* Once the Android emulator is up and running, open a PowerShell prompt.
*   Run this command in PowerShell

    ```
    adb -a -P 5037 nodaemon server
    ```

    * This will start the adb server in the Windows host.
    * Note down the IPV4 address of your Windows host PC/machine.

    **TROUBLESHOOTING:**

    * Sometimes you may get `smartsockets..` error when you run `adb -a -P 5037 nodaemon server` command in PowerShell. In that case, you can do the following steps:
      * Open task manager and kill all `adb` related processes.
      * If Android Studio is open, close it and **keep only** emulator running.
      * If you see a message saying `emulator offline`, **ignore it**.
      * Sometimes, the firewall stops your connection with the host machine. For that, add a firewall rule to allow the connection or check with your organization system admin if using a company machine.
* **Note: Don't close the PowerShell terminal!**
* **Now open your WSL2 terminal and run these commands.**
  * `adb kill-server`
  * `export ADB_SERVER_SOCKET=tcp:<WINDOWS_IPV4_ADDR>:5037`
  * `adb devices`
  * `You should see your connected emulator successfully now.`

### Ready to start Using Maestro?

Yes, at this point, you are free to start your automation.

* [Write your first flow](https://maestro.mobile.dev/getting-started/writing-your-first-flow)
* How to run **Maestro commands**?
  * You can run Maestro commands in WSL2 terminal with `--host` flag. eg.
    * _**maestro --host \<WINDOWS\_IPV4\_ADDR> test flow.yaml**_
    * _**maestro --host \<WINDOWS\_IPV4\_ADDR> studio**_
* Check out the [full documentation](https://maestro.mobile.dev/)

## Known Issue <a href="#2884" id="2884"></a>

```
If your Android emulator is not up and running in the Windows host, the Maestro test
command fails to find the installed emulator.

At this point, it is recommended that you fire up your emulator before running the flow 
using Maestro.
```
