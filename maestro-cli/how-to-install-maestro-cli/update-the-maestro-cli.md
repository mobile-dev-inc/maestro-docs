---
description: Step-by-step update guide for Maestro CLI.
---

# Update the Maestro CLI

Keeping your Maestro CLI up to date ensures you have access to the latest features, command improvements, and security patches. Depending on your original installation method, follow the appropriate steps below.

### Standard update (All platforms)

To upgrade the Maestro CLI to the latest available version on macOS, Linux, or WSL2, run the standard installation script in your terminal:

```bash
curl -fsSL "https://get.maestro.mobile.dev" | bash
```

This command automatically fetches the most recent release and replaces your existing binary.

After running the update, verify that you are running the expected version by checking the CLI metadata:

```bash
maestro --version
```

### Alternative update methods

If you installed Maestro using a package manager or manual download, use these specific commands:

#### **Homebrew (macOS)**

If you used the Homebrew tap, update using the standard brew commands:

```bash
brew update
brew upgrade maestro
```

#### Manual update (Windows)

For native Windows installations not using `curl`:

1. Download the latest [maestro.zip](https://github.com/mobile-dev-inc/maestro/releases/latest/download/maestro.zip) package.
2. Extract the contents into your existing Maestro folder (e.g., `C:\maestro`).
3. Replace all existing files to update the binary.

### Install a specific version

There are scenarios where you may need to downgrade or lock your suite to a specific version for compatibility across a team or CI/CD environment.

To install a specific version, set the `MAESTRO_VERSION` environment variable before running the update script:

```
export MAESTRO_VERSION={version}; curl -Ls "https://get.maestro.mobile.dev" | bash
```

{% hint style="info" %}
You can find a full list of valid versions on the [GitHub releases page](https://github.com/mobile-dev-inc/maestro/releases).
{% endhint %}

You have to pass the version of Maestro CLI you want to install. To do this, replace the `{version}` parameter for your desired Maestro version.

For example, to install the version 2.0.4 opf Maestro CLI:

```bash
export MAESTRO_VERSION=2.0.4; curl -Ls "https://get.maestro.mobile.dev" | bash
```
