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

### macOS

To install on macOS, you can either run:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

Or you can use `homebrew` by running the commands:

```bash
brew tap mobile-dev-inc/tap
brew install maestro
```

{% hint style="warning" %}
For macOS, ensure that your have also the last version os [XCode](https://apps.apple.com/us/app/xcode/id497799835?mt=12) and [XCode Command Line Tools](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools/) installed.
{% endhint %}

### Windows

To install on Windows, you can either run:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

Or you can install using the [releases page on GitHub](https://github.com/mobile-dev-inc/Maestro/releases). To install using the release package, follow this steps:

1. [Download](https://github.com/mobile-dev-inc/maestro/releases/latest/download/maestro.zip) the latest release package.
2. Extract the `.zip` file.
3. Access the folder where you extracted the `.zip` file, for example `C:\Users\User\maestro`.
4. Update your `PATH` to add the Maestro CLI environment variable. You perform this action on Powershell with the comman `setx PATH "%PATH%;C:\Users\jake\maestro\bin"` for the example folder.
5. Run `maestro test` to connect to automatically to any USB device or local emulator.

### Linux

To install on Linux, you can use the `cURL` command on any distribution:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

## Install a specific version of Maestro CLI

You can install a specific version of Maestro CLI to perform your tests. This is usefull to keep the compatibility. To install a specific version of Maestro CLI run:

```bash
export MAESTRO_VERSION={version}; curl -Ls "https://get.maestro.mobile.dev" | bash
```

You have to pass the version of Maestro CLI you want to install. To do this, replace the `{version}` parameter for your desired Maestro version.

For example, to install the version 2.0.4 opf Maestro CLI:

```bash
export MAESTRO_VERSION=2.0.4; curl -Ls "https://get.maestro.mobile.dev" | bash
```

{% hint style="info" %}
To se a list of all the available version, access the [releases page on GitHub](https://github.com/mobile-dev-inc/maestro/releases).
{% endhint %}

## Upgrade the Maestro CLI

To upgrade the Maestro CLI, you can run the follwing command:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

This will upgrade the Maestro CLI to latest version available.
