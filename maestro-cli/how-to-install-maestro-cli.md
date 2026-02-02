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
