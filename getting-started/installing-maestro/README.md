# Installing Maestro

## Installing the CLI

{% hint style="info" %}
**Using Windows?** Follow this guide to get set up on a Windows machine: [Installing Maestro on Windows](windows.md)
{% endhint %}

Run the following command to install Maestro on macOS, Linux or Windows (WSL):

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

If you're on macOS, you can use Homebrew instead of the install script above:

```bash
brew tap mobile-dev-inc/tap
brew install maestro
```

## Upgrading the CLI

Simply run the installation script again:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

## Installing a specific version of Maestro

To install a specific version, export the `MAESTRO_VERSION` environment variable
and run the same installation command as before:

```bash
export MAESTRO_VERSION={version}; curl -Ls "https://get.maestro.mobile.dev" | bash
```

[See the list of available versions](https://github.com/mobile-dev-inc/maestro/releases).

## Installing a specific version of Maestro in a Dockerfile

Define a variable for the version you want to install:

```dockerfile
ENV MAESTRO_VERSION {version}
```

Then download Maestro and add it to your path:

```dockerfile
RUN mkdir -p /opt/maestro && \
wget -q -O /tmp/${MAESTRO_VERSION} "https://github.com/mobile-dev-inc/maestro/releases/download/cli-${MAESTRO_VERSION}/maestro.zip" && \
unzip -q /tmp/${MAESTRO_VERSION} -d /opt/ && \
rm /tmp/${MAESTRO_VERSION}
ENV PATH=/opt/maestro/bin:${PATH}
```

## Connecting to Your Device

`maestro test` will automatically detect and use any local emulator or
USB-connected physical device.

_Note: At the moment, Maestro does not support physical iOS devices_
