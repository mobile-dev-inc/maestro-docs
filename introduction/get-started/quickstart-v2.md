---
hidden: true
---

# QuickStart v2

You are starting your journey with Maestro Studio. This guide will help you install Maestro, set up your environment, and execute your first automated test (called a **Flow**) in just five minutes.

{% stepper %}
{% step %}
### Platform-specific setup

Maestro requires a running target device to execute your tests. Use the tabs below to configure your virtual environment.

{% tabs %}
{% tab title="Android" %}
1. Download the latest version of Android Studio from the [official site](https://developer.android.com/studio) and install it.
2. Open Android Studio, click **More Actions**, and select **Virtual Device Manager**.
3. Click **Create Virtual Device (+)**, select a modern device (e.g., Pixel 8), and download a system image. Maestro supports Android API levels 29, 30, 31, 33, and 34. API 31 or higher is recommended.
4. Finish the wizard and click the **Play** button to start the emulator.
{% endtab %}

{% tab title="iOS" %}
1. Download Xcode from the [Mac App Store](https://apps.apple.com/us/app/xcode/id497799835?mt=12) and install it.
2. Open Xcode, go to `Settings > Locations`, and ensure the **Command Line Tools** are selected.
3. Open Xcode and go to `Xcode > Open Developer Tool > Simulator` to launch the simulator.
4. If no device is available, go to `Xcode > Settings > Platforms` and ensure an iOS runtime is installed. Maestro supports iOS 16, 17, and 18.
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
### Installation

Download the appropriate installer for your operating system:

* **Windows:** [MaestroStudio.exe](https://studio.maestro.dev/MaestroStudio.exe)
* **macOS:** [MaestroStudio.dmg](https://studio.maestro.dev/MaestroStudio.dmg)
* **Linux:** [MaestroStudio.AppImage](https://studio.maestro.dev/MaestroStudio.AppImage)

Follow the platform-specific installation prompts:

* **Windows:** Double-click the `.exe` and follow the setup wizard.
* **macOS:** Open the `.dmg and` drag Maestro Studio to your `Applications` folder.
* **Linux:** Make the `.AppImage` executable (`chmod +x MaestroStudio.AppImage`) and run it with `./MaestroStudio.AppImage --no-sandbox`.
{% endstep %}

{% step %}
### Create your first test

Once your device is running and Maestro Studio is open, you can create your first Flow.

1. Open Maestro Studio and click **Choose new workspace location** to define the directory on your computer to store your tests.

<figure><img src="../.gitbook/assets/quickstart-1 (2).png" alt=""><figcaption></figcaption></figure>

2. Click the **No device connected** button at the top. Select your running Android Emulator or iOS Simulator from the list. The virtual device will popup.
3. Click **Create a new test** to open the setup window.

<figure><img src="../.gitbook/assets/quickstart-create-a-new-test (1).png" alt=""><figcaption></figcaption></figure>

4. On the **Add a new test to your workspace** window, select **Mobile Test** and enter the following:

{% tabs %}
{% tab title="Android" %}
* **Name**: Name for your YAML file.
* **App Id**: From the dropdown menu, select the App Id for testing. For this QuickStart, select **com.android.contacts** from the dropdown menu.

<figure><img src="../.gitbook/assets/quickstart-create-test.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

{% hint style="info" %}
You can also use the **Scan file for App Id** option to automatically detect the identifier from an `.apk` (Android) or `.app/.zip` (iOS) file.

You can also add tags to keep your tests organized.
{% endhint %}

6. Click **Create Test**. Maestro will generate a minimal YAML file to launch the app.

{% tabs %}
{% tab title="Android" %}
```yaml
appId: com.android.contacts
---
- launchApp:
    clearState: true
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
### Run your first test

With your first YAML file created, let's add a few commands to perform a search.

1. In the Maestro Studio editor, copy and paste the example below for your platform.

{% tabs %}
{% tab title="Android (Contacts)" %}
```yaml
appId: com.google.android.contacts    # Target the Contacts app
---
- launchApp:
    clearState: true                  # Start with a clean app state
- tapOn: Create contact               # Open the new contact form
- tapOn: First name                   # Focus the first name field
- inputText: John                     # Enter first name
- tapOn: Last name                    # Focus the last name field
- inputText: Doe                      # Enter last name
- tapOn: Company                      # Focus the company field
- inputText: Maestro                  # Enter company name
- tapOn: back                         # Go back to contact form to add phone
- tapOn: "+1"                         # Open or focus the phone number field
- inputText: 111-111-1111             # Enter phone number
- tapOn: Save                         # Save the new contact
- back                                # Navigate back to contacts list
- takeScreenshot: All Contacts        # Capture a screenshot
```

The test launches the Contacts Android app in a clean state, creates a new contact by filling in first name, last name, and company, adds a phone number, saves the contact, navigates back to the list, and captures a screenshot of all contacts.

{% hint style="info" %}
To learn more about the commands you can use to create tests, access the [Commands overview](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/ "mention")page.

To learn about how you can structure tests, also reference in Maestro as Flows, access the [Maestro Flows overview](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/ "mention").
{% endhint %}

After pasting, click **Run Locally**. Watch your virtual device execute the steps automatically. Maestro Studio will highlight each step as it succeeds or provide a reason for failure if an element cannot be found.

(adjust example below)

<figure><img src="../.gitbook/assets/first-test-quickstart-android.gif" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="iOS (Safari)" %}
```
```
{% endtab %}
{% endtabs %}


{% endstep %}
{% endstepper %}

#### Interactive Flow  authoring

While this Quickstart focuses on writing commands manually in the YAML file, Maestro Studio offers three ways to build your test:

* **Insert Command**: Click the **Insert Command** button in the IDE to choose from a list of standard actions.
* Manual Entry: Type commands directly into the YAML editor for precise control.
* Inspect Screen: Click the **Inspect Screen** button to select elements visually on the device and receive recommended commands

<figure><img src="../.gitbook/assets/quickstart-explore-options.gif" alt=""><figcaption></figcaption></figure>

### Video walkthrough

Watch this step-by-step video to see the first test creation process in detail:

{% embed url="https://www.youtube.com/watch?v=E7qwFwo_nu0" %}

### Next steps

Now that you’ve seen the power of "arm's length" automation, explore these resources to master the ecosystem:

* Visit the [Maestro Studio overview](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/ "mention") to learn how to use visual element inspection and the Live REPL to build tests without writing code from scratch.
* If you prefer a programmatic approach or need to integrate tests into your CI/CD pipeline, head to the [Maestro CLI overview](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/ "mention").
* To learn the best practices for logic, modularity, and nesting, check out the  [Maestro Flows overview](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/ "mention").

You can also learn how to [organize your repository](https://www.google.com/search?q=https://docs.maestro.dev/get-started/repository-config) for scalable testing or use the [Maestro MCP Server](https://www.google.com/search?q=https://docs.maestro.dev/get-started/maestro-mcp) to enable AI tools like Claude or Cursor to help build your tests.
