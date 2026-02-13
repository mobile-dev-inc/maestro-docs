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

Now it is time to build the Flow. Instead of manual typing, we will use the IDE's interactive features.

First, click **Insert Command**, search for the `startRecording` command, and select it. This step will record the device screen during the test.

To add the following steps, use **Inspect Screen** to add commands based on your interaction with the app:

1. Click the **Inspect Screen** button.
2. **Allow notifications**: Click the **Allow** button on the device screen. Maestro will suggest a command; select `tapOn: Allow`.
3. **Note**: Disable **Inspect Mode** to interact with the device again and click **Allow** manually. You must repeat this "inspect then interact" process for each step.
4. **Create Contact**: Use **Inspect Screen** on the **Create contact** button and select `tapOn: Create contact`.
5. **First Name**: Inspect the **First name** field and select `tapOn`. Immediately follow this by using **Insert Command** to add `inputText`, replacing `"Hello world"` with `"Jane"`.
6. **Last Name**: Inspect the **Last name** field, select `tapOn`, and use **Insert Command** to add `inputText`, replacing `"Hello world"` with `"Doe"`.
7. **Phone**: Use **Insert Command** to add `tapOn: "+1"` to select the phone field. Immediately follow this with `inputText`, replacing `"Hello world"` with `"111-111-1111"`.
8. **Save**: Inspect the **Save** button and select `tapOn: Save`.
9. **Confirmation**: Use **Insert Command** to add the `back` command to return to the list, and finally add `stopRecording` to save the test video.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FeQi66gxHTt2vx4HjhM9V%2Fuploads%2Fpa1PNWe7SRhirsart2Lq%2Fcreate-flow.mp4?alt=media&token=0d37763d-2534-4e20-9d42-3a969383caaf" %}
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
- inputText: 111-111-1111
- tapOn: Save
- back
- stopRecording
```

Click **Run Locally** to watch Maestro Studio execute these steps automatically on your device.

<figure><img src=".gitbook/assets/2026-02-12_22-30-00.gif" alt=""><figcaption></figcaption></figure>

After a successful run, the recording file will be available in the `.maestro` directory.
{% endstep %}
{% endstepper %}

### Next steps

Now that you have created a Flow using the interactive features of Maestro Studio, you can explore more advanced capabilities:

* [Environments and variables](environments-and-variables.md): Learn how to pass dynamic data like names or phone numbers using variables.
* [Run cloud tests from Maestro Studio](run-cloud-tests-from-maestro-studio.md): Learn how to execute this Flow on using Maestro Cloud.

To learn more about test structure and advanced logic, visit the [Maestro Flows documentation](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/).
