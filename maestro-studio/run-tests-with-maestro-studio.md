---
description: >-
  Build and run mobile tests visually with Maestro Studio. Install the app,
  create tests via screen inspection, and automate without writing code from
  scratch.
---

# Run tests with Maestro Studio

Maestro Studio is a visual desktop app that simplifies mobile test automation. This guide covers how to install the application and use its interactive tools to build a contact-creation test without writing code from scratch.

### Prerequisites&#x20;

Before building your test, ensure you have a running Android emulator. Access the [QuickStart](https://app.gitbook.com/s/CbCMt5C3rawmE9oIus7f/get-started/quickstart) for further guidance on setting up your virtual environment.&#x20;

{% stepper %}
{% step %}
### Installation

Get started by downloading the installer for your specific operating system:

* **Windows**: Download [MaestroStudio.exe](https://studio.maestro.dev/MaestroStudio.exe) and follow the setup wizard.
* **macOS**: Download [MaestroStudio.dmg](https://studio.maestro.dev/MaestroStudio.dmg) and drag the icon into your Applications folder.
* **Linux**: Download [MaestroStudio.AppImage](https://studio.maestro.dev/MaestroStudio.AppImage), make it executable with `chmod +x`, and run it.
{% endstep %}

{% step %}
### Initial setup

1. Launch Maestro Studio.
2. Click **New workspace** to select a folder on your machine where your test files will be saved.&#x20;

<figure><img src=".gitbook/assets/create workspace.gif" alt=""><figcaption></figcaption></figure>

3. Click on **Select device** at the top left and select your active virtual device from the list.

<figure><img src=".gitbook/assets/connect device.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Create the test file



1. Click **New File.**
2. Enter a name for your test file, for example `my_test.yaml`.
3. Select your app from the dropdown menu.
4. Click **Create Test**.

{% hint style="info" %}
Tags are used to control which tests run. For more information, access the following pages:

* [environments-and-variables.md](environments-and-variables.md "mention")
* [run-cloud-tests-from-maestro-studio.md](run-cloud-tests-from-maestro-studio.md "mention")
{% endhint %}

<figure><img src=".gitbook/assets/create new file.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Test the app initialization

Before you begin building the test, run the app initialization. Click **Run Test** and observe the app initializing with a clear state.

<figure><img src=".gitbook/assets/run test_launch app.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Build your test

The fastest way to build a test is to **right-click directly on any element** in your app. A menu appears with the available Maestro commands for that element. Click the one you want, and it gets added to your test automatically.

<figure><img src=".gitbook/assets/test creation_1.gif" alt=""><figcaption></figcaption></figure>

You can also type a hyphen in the editor to see all available Maestro commands.

<figure><img src=".gitbook/assets/test__2.gif" alt=""><figcaption></figcaption></figure>

Autocomplete suggests commands, arguments, and real selectors from your connected device's screen, so you spend less time looking up syntax.

<figure><img src=".gitbook/assets/test__4.gif" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
### Review and run the test

Once your first test is ready, click **Run Test** to watch Maestro Studio execute these steps automatically on your device.

<figure><img src=".gitbook/assets/run.gif" alt=""><figcaption></figcaption></figure>

After a successful run, the recording file will be available in the `.maestro` directory.
{% endstep %}
{% endstepper %}

### Next steps

Now that you have created a test using the interactive features of Maestro Studio, you can explore more advanced capabilities:

* [Environments and variables](environments-and-variables.md): Learn how to pass dynamic data like names or phone numbers using variables.
* [Run cloud tests from Maestro Studio](run-cloud-tests-from-maestro-studio.md): Learn how to execute this test on using Maestro Cloud.

To learn more about test structure and advanced logic, visit the [Maestro Flows documentation](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/).
