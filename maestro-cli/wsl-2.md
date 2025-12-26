# How to setup Maestro with WSL2

Maestrou studio allows your to use WSL2 when using Windows.

### Pre-Requisites

1. PowerShell installed.
2. Android Studio installed.
3. Add `ANDROID_HOME` to Windows `PATH`.
   a. To check if your `ANDROID_HOME` is on the Windows `PATH`, open a PowerShell terminal and run this command `adb --version.`
4. Install Java JDK 17 or higher and set `JAVA_HOME`.
   a. Run `java -version` to check if Java 17+ is installed correctly.

## Instal WSL2

In order to install the Windows Subsystem for Linux (WSL2) open a terminal on Windows and run the command:

```bash
wls --install
```

{% hint title="warning" %}
This command will install Ubuntu by default.
{% endhint %}

{% hint title="success" %}
For a better experience using the WSL2 on Windows 11, instal the new [Terminal](https://github.com/microsoft/terminal).
{% endhint %}

After the installation is completed, the terminl will open automatically. Enter your desired username and password for the new Ubuntu installation.

{% hint title="success" %}
After install Ubuntu with the command above, run:

```bash
sudo apt update
sudo apt upgrade
```
This will upgrade your installation.
{% endhint %}

## Install Java

After installint rebooting and upgrade the new WSL2 installation, you have to install Java to run Maestro CLI. To do this, run the command:

```bash
sudo apt install openjdk-17-jdk
```

This will install the versjon 17 of Java JDK.

## Instal Maetro CLI

To install the Maestro CLI on WSL2, run the command:

```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
```

To check your Maestro installation, run:

```bash
maestro --version
```