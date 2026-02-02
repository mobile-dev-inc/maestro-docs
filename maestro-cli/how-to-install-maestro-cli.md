# How to install Maestro CLI

Maestro also provides you with the option to use the CLI by terminal. This document will cover the installation of Maestro CLI on the three operational system supported: macOS, Windows and Linux.

## Prerequisites

To install the Maestro CLI, you need the following:

* Java version 17 or higher.

{% hint style="warning" %}
- Ensure that the `JAVA_HOME` environment variable points to your Java 17+ installation.
- You can install Java using [Oracle JDk](https://www.oracle.com/java/technologies/downloads/), [OpenJDK](https://openjdk.org/install/) or [SDKMAN](https://sdkman.io/).
- To verify the version os your Java installation, run `java --version`.
{% endhint %}

## Installation

You can install the Maestro CLI on Windows, macOS and Linux.

{% tabs %}
{% tab title="macOS" %}
To install on macOS, you can either run:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

Or you can use `homebrew` by running the commands:

```bash
brew tap mobile-dev-inc/tap
brew install maestro
```

Run `maestro --help` to verify that the Maestro CLI is working properly.

{% hint style="warning" %}
For macOS, ensure that your have also the last version os [XCode](https://apps.apple.com/us/app/xcode/id497799835?mt=12) and [XCode Command Line Tools](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools/) installed.
{% endhint %}
{% endtab %}

{% tab title="Windows" %}
To install on Windows, you can either run:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

Or you can install using the [releases page on GitHub](https://github.com/mobile-dev-inc/Maestro/releases). To install using the release package, follow these steps:

1. Download the latest [maestro.zip](https://github.com/mobile-dev-inc/maestro/releases/latest/download/maestro.zip).
2. Extract the content to a stable location (e.g., `C:maestro`).
3.  Update your `PATH` to add the Maestro CLI environment variable. Run the following in PowerShell to add the Maestro `bin` folder to your environment variables:<br>

    ```powershell
    setx PATH "%PATH%;C:\maestro\bin"
    ```
4. Restart your terminal to apply changes.

Run `maestro --help` to verify that the Maestro CLI is working properly.
{% endtab %}

{% tab title="Windows (WSL)" %}
Installing Maestro in WSL2 allows you to use a Linux environment while using Android emulators running on your Windows host.

#### 1. Install Java and Maestro

First, ensure you have Java 17+ installed.

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

Update your environment variables to ensure `JAVA_HOME` is set and Maestro is in your `PATH`. Add the following to your `~/.bashrc` (or `~/.zshrc`):

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
export PATH=$PATH:$HOME/.maestro/bin
```

Reload your configuration:

```bash
source ~/.bashrc
```

Now, install Maestro:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

#### 2. Setup Android environment

Since you cannot run the Android Studio GUI directly in WSL easily, you need to set up the Android command-line tools manually. This enables you to access and control the Android emulator running on Windows.

1.  Create the Android directory:

    ```bash
    mkdir -p $HOME/Android/cmdline-tools
    ```
2.  Download the latest [command line tools for Linux](https://developer.android.com/studio#command-tools) (zip/targz) and unzip it. Make sure you update the URL with the latest version.

    ```bash
    cd $HOME/Android/cmdline-tools
    # Replace with the actual URL for the latest version
    wget https://dl.google.com/android/repository/commandlinetools-linux-14742923_latest.zip -O cmdline-tools.zip
    unzip cmdline-tools.zip
    mv cmdline-tools latest
    rm cmdline-tools.zip
    ```
3.  Configure the environment by adding the following to your `~/.bashrc`:

    ```bash
    # --- Android PATH ---
    export ANDROID_HOME=$HOME/Android
    export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
    export PATH=$PATH:$ANDROID_HOME/platform-tools
    ```
4.  Reload the terminal running:

    ```bash
    source ~/.bashrc.
    ```
5.  Install the platform tools:

    ```bash
    sdkmanager --install "platform-tools"
    ```

#### 3. Connect to Windows Emulator

Android Emulators run on the Windows host. You need to bridge ADB from WSL to Windows.

**On Windows (PowerShell):**

Start the ADB server to allow external connections.&#x20;

```powershell
adb -a -P 5037 nodaemon server
```

If successful, the command will not show any output and will just sit there. This is normal! Do not close this PowerShell window, as it keeps the connection alive.

After starting the server and proceeding to WSL, you must have an active Android device. To accomplish this:

1. Open Android Studio on Windows.
2. Launch a Virtual Device using the Emulator.

{% hint style="info" %}
#### `adb` is not recognized?

If you see an error saying `The term 'adb' is not recognized`, it means the Android SDK platform-tools are not in your Windows PATH.

**Add to PATH via PowerShell (Recommended)**

Run this command in PowerShell to permanently add the path for your user:

```powershell
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";$env:LOCALAPPDATA\Android\Sdk\platform-tools", "User")
```

Restart your PowerShell terminal after running this command.

**Manual method**

1. Search for **Edit environment variables for your account** in Windows Search.
2. Edit the `Path` variable.
3. Click **New** and paste: `%LOCALAPPDATA%\Android\Sdk\platform-tools`.
{% endhint %}

{% hint style="info" %}
#### Error: could not install `smartsocket` listener?

If you see an error like `cannot bind to 0.0.0.0:5037`, it means another ADB (e.g., from Android Studio) is already running. To solve this problem, do the following:

1. Close Android Studio.
2.  Kill the existing process running:

    ```powershell
    taskkill /F /IM adb.exe
    ```
3. Try to start the ADB server again.
{% endhint %}

**On WSL:**

Configure ADB to connect to the Windows host IP. Replace `<WINDOWS_IP>` with your actual Windows IP address.

```bash
adb kill-server
export ADB_SERVER_SOCKET=tcp:<WINDOWS_IP>:5037
adb devices
```

{% hint style="success" %}
To identify the `WINDOWS_IP`, run the following command in yout WSL terminal:

```bash
ip route show | grep default | awk '{print $3}'
```
{% endhint %}

You should see your emulator listed, indicating your connection is working.&#x20;

#### 4. Running Maestro

When running Maestro commands, use the `--host` flag to point to your Windows machine:

```bash
maestro --host <WINDOWS_IP> test flow.yaml
```
{% endtab %}

{% tab title="Linux" %}
To install on Linux, you can use the `cURL` command on any distribution:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

Run `maestro --help` to verify that the Maestro CLI is working properly.
{% endtab %}
{% endtabs %}

## Install a specific version of Maestro CLI

You can install a specific version of Maestro CLI to perform your tests. This is useful to keep the compatibility. To install a specific version of Maestro CLI run:

```bash
export MAESTRO_VERSION={version}; curl -Ls "https://get.maestro.mobile.dev" | bash
```

You have to pass the version of Maestro CLI you want to install. To do this, replace the `{version}` parameter for your desired Maestro version.

For example, to install the version 2.0.4 opf Maestro CLI:

```bash
export MAESTRO_VERSION=2.0.4; curl -Ls "https://get.maestro.mobile.dev" | bash
```

{% hint style="info" %}
To see a list of all the available version, access the [releases page on GitHub](https://github.com/mobile-dev-inc/maestro/releases).
{% endhint %}

## Upgrade the Maestro CLI

To upgrade the Maestro CLI, you can run the following command:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

This will upgrade the Maestro CLI to latest version available.
