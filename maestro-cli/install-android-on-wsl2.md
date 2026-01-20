# Install Android on WSL2

You can use the Android development kit with WSL2 and Mestro.

## Prerequisites

* Android command line tools.
  * Download from the official Android Studio site.

## Install Android command line tools

To install the Android command line tools, follow the steps:

1,. Unzip the Android Command Line Tools file:

```bash
unzip <android-filename.zip>
```

2. Create a directory on your home:

```bash
mkdir Android
```

3. Move the Android command line tools the latests directory:

```bash
mkdir latest
mv cmdline-tools/* latest/
mv latest/ cmdline-tools/
```

3. Add the Android command line tools to the `.bashrc`:

{% hint style="info" %}
To open your `.bashrc` file, use a text editor like VIM (Vi IMproved) or NANO (Nano's ANOther editor), for example: `nano .bashrc`.
{% endhint %}

```bash
export ANDROID_HOME=$HOME/Android
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
```

4. Save your `.bashrc` and exit.
5. Reload your `.bashrc`:

```bash
source ~/.bashrc
```

6. Install the basic Android utilities using Android command line tools:

```bash
sdkmanager --install plataform-tools
```

7. Add the new directory to your `.bashrc`:

```bash
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

8. Reload your `.bashrc`:

```bash
source ~/.bashrc
```

9. Check if everything is working fine:

```bash
adb --version
```

10. Launch your Android emulator and run the command:

```bash
adb -a -P 5037 nodaemon server
```

This starts the Android Debug Bridge (ADB) server on your Windows machine. Take note of the IPv4 address of your Windows host.
