---
description: >-
  Build and run mobile tests visually with Maestro Studio. Install the IDE,
  create Flows via screen inspection, and automate tests without writing code.
---

# Run tests with Maestro Studio

Maestro Studio is a visual IDE that simplifies mobile automation. This guide covers how to install the application and use its interactive tools to build a contact-creation Flow without writing code from scratch.

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
2. Click **Choose new workspace location** to select a folder on your machine where your test files will be saved.
3. Click the **No device connected** status at the top and select your active virtual device from the list.

<figure><img src=".gitbook/assets/conect-device.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Create the Flow

Now you can create your first test. In this example, we will build a Flow for the **Android Contacts** app using Maestro's visual tools:

1. Click **Create a new test** and select **Mobile Test**.
2. Enter `create_contact.yaml` as the Flow name.
3. Select `com.google.android.contacts` from the dropdown menu.
4. Add `android` as a tag for the test.
5. Click **Create Test**. This generates a basic Flow that targets the app.

{% hint style="info" %}
Tags are used to control which tests run. For more information, access the following pages:

* [environments-and-variables.md](environments-and-variables.md "mention")
* [run-cloud-tests-from-maestro-studio.md](run-cloud-tests-from-maestro-studio.md "mention")
{% endhint %}

<figure><img src=".gitbook/assets/create-test (1).gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Test the app initialization

Before you begin building the Flow logic, test the app initialization. Click **Run Locally** and observe the app initializing with a clear state.

<figure><img src=".gitbook/assets/test-inicialization.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Interactive authoring&#x20;

Now it is time to build the Flow logic. Instead of manual typing, we will use **Insert Command** and **Inspect Screen** features to build the steps.

First, click **Insert Command**, search for the `startRecording` command, and select it. This will record the device screen during the test execution.

To build the following steps of your Flow, use **Inspect Screen** to select the element and use the **Run and Insert** action to build the test as you go:

1. **Allow notifications**: Click **Inspect Screen**, click the **Allow** button on the device, and select **Run and Insert** for `tapOn: Allow`. This executes the tap on your device and adds the command to your YAML.
2. **Create Contact**: Click the **Create contact** button on the device and select **Run and Insert** for `tapOn: Create contact`.
3. **First Name**: Click the **First name** field, select **Run and Insert** for `tapOn`. Use **Insert Command** to add `inputText`, replacing the default text with `"Jane"`.
4. **Last Name**: Click the **Last name** field, select **Run and Insert** for `tapOn`, and use **Insert Command** to add `inputText` with the value `"Doe"`.
5. **Phone**: Use **Insert Command** to add `tapOn: "+1"` to select the phone field. Use **Insert Command** to add `eraseText` to clear any default formatting, then add `inputText` with the value `"+1 111-111-1111"`.
6. **Save**: Click the **Save** button and select **Run and Insert** for `tapOn: Save`.
7. **Confirmation**: Use **Insert Command** to add `back` to return to the list, then add `stopRecording` to save the test video.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FeQi66gxHTt2vx4HjhM9V%2Fuploads%2FG2Ah0XbkirPXZIV6jLqJ%2Fcreate-test-maestro-studio-ezgif.com-video-speed%20(1).mp4?alt=media&token=0928ec82-7d19-4359-809a-5fa24f4640a6" %}
{% endstep %}

{% step %}
### Review and run the Flow

Your completed `create_contact.yaml` should look like this:

```yaml
appId: com.google.android.contacts
tags:
  - android
---
- launchApp:
    clearState: true
- startRecording: recording
- tapOn: Allow
- tapOn: Create contact
- tapOn: First name
- inputText: Jane
- tapOn: Last name
- inputText: Doe
- tapOn: "+1"
- eraseText
- inputText: "+1 111-111-1111"
- tapOn: Save
- back
- stopRecording
```

Click **Run Locally** to watch Maestro Studio execute these steps automatically on your device.

<figure><img src=".gitbook/assets/2026-02-16_08-42-49.gif" alt=""><figcaption></figcaption></figure>

After a successful run, the recording file will be available in the `.maestro` directory.
{% endstep %}
{% endstepper %}

### Next steps

Now that you have created a Flow using the interactive features of Maestro Studio, you can explore more advanced capabilities:

* [Environments and variables](environments-and-variables.md): Learn how to pass dynamic data like names or phone numbers using variables.
* [Run cloud tests from Maestro Studio](run-cloud-tests-from-maestro-studio.md): Learn how to execute this Flow on using Maestro Cloud.

To learn more about test structure and advanced logic, visit the [Maestro Flows documentation](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/).
