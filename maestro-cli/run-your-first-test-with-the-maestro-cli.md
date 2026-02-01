# Run your first test with the Maestro CLI

In this tutorial, you will write and run your first Maestro Flow using Maestro CLI. This tutorial creates a test to validate the contact creation in a Android device using the Contacts app

### Prerequisites

Before starting, ensure you have the following:

* **Maestro CLI**: Installed on your machine. Access [how-to-install-maestro-cli.md](how-to-install-maestro-cli.md "mention")if it's not installed in your machine yet.&#x20;
* **Android Studio**: Installed to manage emulators. Check the [QuickStart](https://mobile-dev-1.gitbook.io/docs-vnext/get-started/quickstart).

{% stepper %}
{% step %}
### Start the Android emulator

Maestro needs a running device to interact with. This example uses an Android Emulator for this tutorial.

1. Open **Android Studio**.
2. Go to the **Virtual Device Manager**.
3. Launch a virtual device (e.g., Pixel 8 or similar).

<figure><img src=".gitbook/assets/run-maestro-cli-1.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Create the Flow

{% hint style="info" %}
This tutorial uses the system's default Contacts app (`appId: com.google.android.contacts`), which comes pre-installed on standard Android emulators. You don't need to install any external app for this tutorial.
{% endhint %}

A Flow in Maestro is a YAML file that contains all the instruction Maestro must execute to complete the test. For more information about how to create Flows, access the [Flows](https://app.gitbook.com/o/zCVYm3M93B0sOcjR1Oj4/s/mS3lsb9jRwfRHqddeRXG/ "mention")documentation. For this example, follow the steps:

1. Create a new file named `contacts.yaml` in your working directory.
2. Copy and paste the following content into the file:

```yaml
appId: com.google.android.contacts
---
- launchApp:
    clearState: true
- startRecording: recording   
- tapOn: Allow
- tapOn: Create contact
- tapOn: First name
- inputRandomPersonName
- tapOn: Last name
- inputRandomPersonName
- tapOn: Company
- inputText: Maestro
- tapOn: "+1"
- inputText: 111-111-1111
- tapOn: Save
- back
- stopRecording
```
{% endstep %}

{% step %}
### Run the Flow

Now, let's see Maestro in action.

1. Open your terminal.
2. Navigate to the directory where you saved `contacts.yaml`.
3. Run the following command:

```bash
maestro test contacts.yaml
```

Maestro will start running the test. At the end your terminal should show that all steps were executed sucessufully.

<figure><img src=".gitbook/assets/cli-running-test.png" alt=""><figcaption></figcaption></figure>

Maestro will connect to your running emulator and execute the steps one by one. You should see:

1. Maestro start recording the scrren and the Contacts app opens.
2. A new contact form is opened.
3. Random names and a phone number are typed in.
4. The contact is saved.
5. After displaying the saved contact info, the `back` command is used to return to the full contact list
6. to finish, maestro stop recording the screen and a file `recording.mp4` is saved in the same directory as the `contacts.yaml` file.
{% endstep %}
{% endstepper %}

### Outcome

After following the above steps, you should have a file`recording.mp4` is saved displaying the complete process, as the one below:

<figure><img src=".gitbook/assets/running-cli-example-maestro.gif" alt="" width="270"><figcaption></figcaption></figure>

