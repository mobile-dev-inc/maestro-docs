# Install a specific Maestro CLI version

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
