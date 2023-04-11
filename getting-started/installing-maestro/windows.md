---
description: A step by step guide to install Maestro in Windows
---

# Windows

Maestro works great on Windows computers, but there are a few unique setup steps to be aware of. This guide will walk you through the end-to-end steps for getting started with Maestro on a Windows machine.

### Pre-Requisites

1. Powershell is installed in Windows system.
2. Install android studio in windows machine.
3. Add ANDROID\_HOME to your windows environment variable.
   1. To check if your ANDROID\_HOME setup is correctly done, open a powershell terminal and run this command `adb --version.`
   2. Note down the adb version.
4. Install Java JDK 11 and set JAVA\_HOME
   1. Run `java  --version` to check if the java is installed correctly.

## Steps <a href="#8b4a" id="8b4a"></a>

1. Install WSL2 (Window Subsystem for Linux)
2. Install Java 11
3. Install Maestro

## 1. Install WSL 2 <a href="#0215" id="0215"></a>

With recent Windows 11, Microsoft have made it pretty easy to install Windows Subsystem For Linux aka WSL

In order to install WSL, open Powershell As Administrator and run following command:

```bash
wsl --install
```

After running the above command, follow through instructions and restart the computer.

Install [Windows Terminal](https://github.com/microsoft/terminal) application for refreshing terminal experience.

Set your linux username and password (Something that you will not forget).

Run following 2 commands to update your Ubuntu system. Enter password when prompted.

```bash
sudo apt update
sudo apt upgrade
```

## 2. Install Java <a href="#5521" id="5521"></a>

After restarting the system, open Terminal application and click on the dropdown to select Ubuntu. Type in following command:

```bash
sudo apt install openjdk-11-jdk
```

## 3. Install Maestro

Installing Maestro is now just a matter of running following one command.

```
     curl -Ls "https://get.maestro.mobile.dev" | bash
```

**TADA!**

**You have successfully installed Maestro in your Windows machine** 🙌

Check your maestro version using following command

```bash
maestro --version
```

## What Next? <a href="#7639" id="7639"></a>

### Let's set you up to use android in your freshly installed WSL2



* Download android command line tools zip file from [android official site.](https://developer.android.com/studio)
*   Use the following instructions to setup android command lines correctly in your WSL2 .

    * Open WSL2 terminal.
    * Install JDK using following command `sudo apt install default-jdk`
    * Create a new directories in your home directory.

    ```
    ~ $ mkdir Android
    ~ $ cd Android
    ```

    * Unzip the android command line tools zip file in the `android` directory using this command: `unzip ~<command_line_zip_filename>.zip`
    * In the `android` directory:

    ```
    $ cd cmdline-tools
    $ mkdir tools
    $ mv -i * tools
    ```

    **Note:** Last command will probably give you a warning, but you don’t need the worry about that.

    * Now add the following line to your `~/.bashrc` file:

    ```
    export ANDROID_HOME=$HOME/Android
    export PATH=$PATH:$ANDROID_HOME/tools/bin
    ```

    * Run `source ~/.bashrc` to reload the bashrc file.
    * Run `sdkmanager --list` to check if everything is working fine.
    * Run `sdkmanager --install "platform-tools"` to install platform tools.
    * To check that everything went good, do following:
      * Close and relaunch terminal
      * Run `adb --version` and see that adb version is shown
      * Since everything is installed fresh, your WSL 2 adb version should perfectly match with windows adb version that we noted down as part of pre-requisites.



**Please follow below steps to setup the ADB and make sure you are able to use android emulators with your WSL2 correctly**

* Fire up your android emulator on windows.
* Once android emulator is up and running, open a POWERSHELL PROMPT.
*   Run this command in Powershell

    ```
    adb -a -P 5037 nodaemon server
    ```

    * This will start the adb server in windows host.
    * Note down the IPV4 address of your windows host PC/machine.

    **TROUBLESHOOTING:**

    * Sometimes you may get `smartsockets..` error when you run `adb -a -P 5037 nodaemon server` command in powershell. In that case you can do following steps:
      * Open task manager and kill all `adb` related processes.
      * If Android studio is open, close it and KEEP ONLY emulator running.
      * If you see a message saying `emulator offline`, IGNORE IT.

    \

* **Note: Don't close the powershell terminal.!!**
* **Now open your WSL2 terminal and run these commands.**
  * `adb kill-server`
  * `export ADB_SERVER_SOCKET=tcp:<WINDOWS_IPV4_ADDR>:5037`
  * `adb devices`
  * `You should see your connected emulator successfully now.`



### Ready to start Using Maestro?

Yes at this point you are free to start your automation.

* [Write your first flow](https://maestro.mobile.dev/getting-started/writing-your-first-flow)
* How to run **Maestro commands**?
  * You can run maestro commands in WSL2 terminal with `--host` flag. eg.
    * _**maestro --host \<WINDOWS\_IPV4\_ADDR> test flow.yaml**_
    * _**maestro --host \<WINDOWS\_IPV4\_ADDR> studio**_
* Check out the [full documentation](https://maestro.mobile.dev/)

## Known Issue <a href="#2884" id="2884"></a>



```
If your android emulator is not up and running in windows host, the maestro test
command fails to find installed emulator.
At this point it is recommended that you fire up emulator before running the flow 
using maestro.
```
