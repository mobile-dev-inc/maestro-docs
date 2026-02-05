---
description: >-
  Create YAML test flows in Maestro Studio. Select a device, add commands via
  Insert Command, Inspect Screen, or write YAML directly, then Run Locally.
---

# How to create tests with Maestro Studio

To run tests with Maestro Studio, you just need to create a YAML file with the test flow. But first, you need to set up your environment for the platform you are developing for (Android, iOS, or Web).

## Prerequisites

* [Maestro Studio installed](/broken/pages/Gkh2PaXSFN0gAJQLxuIc)

**For Android tests**

* [Android Studio](https://developer.android.com/studio/install).
* [Android Virtual Device (emulator) configured](https://developer.android.com/studio/run/emulator#avd).

**For iOS tests**

* [XCode installed](https://apps.apple.com/us/app/xcode/id497799835?mt=12).
* [XCode command line tools installed](https://developer.apple.com/xcode/resources/).

{% hint style="success" %}
The XCode already provides a simulator, if you need to install a differente one than the default, follow the instructions on the Apple Official documentation: [Adding additional simulators](https://developer.apple.com/documentation/safari-developer-tools/adding-additional-simulators).
{% endhint %}

## Creating your first YAML file

Once you have installed and set up your development environment, you can proceed to Maestro Studio and start creating your first YAML file.

1. Open Maestro Studio.
2. Click the **No device connected** button to open the panel.

![Open the device selection panel](.gitbook/assets/no-device.png)

3. On the panel, selecte the device you want to run your tests.
4. On the Maestro Studio, click **New Test** option to open the **Add a new test to your workspace** window.
5. On the **Add a new test to your workspace** window, select the type of test (Mobile Test, Web Test, or JavaScript File), and fill in:
   * **Name**: Name for your YAML file.
   * **App Id**: From the dropdown menu, select the App Id for testing.
     * You can also click the **Scan file for App Id** option. This allows you to indicate an app file to test (such as an `.apk` for Android or a `.zip` for iOS).
   * **Tags**: Add tags to your tests to keep them organized.
6. Click **Create Test** to create the YAML file.

![Create your first test](.gitbook/assets/workspace-test.png)

Maestro Studio creates a clean and minimal test file:

```yaml
appId: https://docs.maestro.dev/
tags:
  - First Test
---
- launchApp:
    clearState: true
```

## Add commands to your test flow

With your first YAML file created, you can start building the test itself. To do this, add actions to your file by clicking the **Insert Command** button in the IDE, typing the command in the YAML file, or clicking the **Inspect Screen** button.

### Add commands using the insert command option

To add commands this way, click the **Insert Command** button in the IDE. This opens a dropdown menu with options to add. For example, add a `tapOn` command to simulate a tap on an element called `Login`.

The YAML file should look like this:

```yaml
appId: https://docs.maestro.dev/
tags:
  - First Test
---
- launchApp:
    clearState: true
- tapOn: Login
```

### Add commands using inspect screen option

To add commands this way, click the **Inspect Screen** button. This takes you to the screen of the device you're testing, where you can select the coordinates of an element to test it.

The YAML file should look like this:

```yaml
appId: https://docs.maestro.dev/
tags:
  - First Test
---
- launchApp:
    clearState: true
- tapOn:
    id: Open table of contents
```

### Add commands using YAML

You can also write your commands directly in the YAML file. The syntax and commands are the same, but you will not have visual feedback.

```yaml
appId: https://docs.maestro.dev/
tags:
  - First Test
---
- launchApp:
    clearState: true
- tapOn:
    id: Open table of contents
```

## Run your test

To run your first test, after creating the YAML file, click **Run Locally** at the top of Maestro Studio and wait for the result.

The example below runs a test with the Maestro documentation site. The test consists of:

1. Navigate to the Maestro documentation site at `https://docs.maestro.dev/`.
2. Open the table of contents of the documentation site.
3. Select the **Run a Sample Flow** article.
4. Take a screenshot of the article on the documentation site.

The YAML file should look like this:

```yaml
appId: https://docs.maestro.dev/
tags:
  - First Test
---
- launchApp:
    clearState: true
- tapOn:
    id: Open table of contents
- tapOn: Run a Sample Flow
- takeScreenshot: MainScreen
```

The screenshot is saved inside the `.maestro/screenshots` folder. You can copy and paste it to run as a simple example using a web browser (Chromium).
