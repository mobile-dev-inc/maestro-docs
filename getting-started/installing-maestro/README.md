# Installing Maestro

## Installing the CLI

{% hint style="info" %}
**Using Windows?** Follow this guide to get set up on a Windows machine: [Installing Maestro on Windows](windows.md)
{% endhint %}

Run the following command to install Maestro on Mac OS, Linux or Windows (WSL):

```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
```

## Upgrading the CLI

Simply run the installation script again:

```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
```

## Installing a specific version of Maestro

To install a specific version, declare a `MAESTRO_VERSION` property and run the same installation command as before:

```bash
export MAESTRO_VERSION={version}; curl -Ls "https://get.maestro.mobile.dev" | bash
```

## Connecting to Your Device

{% tabs %}
{% tab title="iOS" %}
Before running Flows on iOS Simulator, install [Facebook IDB](https://fbidb.io/) tool

```shell
brew tap facebook/fb
brew install facebook/fb/idb-companion
```



_Note: At the moment, Maestro does not support real iOS devices_
{% endtab %}

{% tab title="Android" %}
`maestro test` will automatically detect and use any local emulator or USB-connected physical device.
{% endtab %}
{% endtabs %}

### Homebrew support

We no longer recommend using homebrew to manage your maestro installation and instead recommend the installation script above. To upgrade your maestro installation that was installed via Homebrew we recommend uninstalling it and then reinstalling it using the official instructions:

```bash
brew uninstall maestro
curl -Ls "https://get.maestro.mobile.dev" | bash
```
