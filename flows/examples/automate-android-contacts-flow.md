# Automate Android Contacts Flow

Testing how your app interacts with system contacts, or simply testing the native Contacts app itself, is a great way to explore Maestro's ability to handle system-level applications. This example demonstrates how to create a new contact from scratch, utilizing Maestro's built-in data generation to ensure every test run is unique.

### The Workflow

Since you will be interacting with a system app, the Flow focuses on navigating on the standard Android UI patterns and handling keyboard states.

1. Launch the target the native Android contacts package.
2. Use Maestro built-in commands to create realistic names, phone numbers, and emails on the fly.
3. Use the `back` command to dismiss the soft keyboard when it obstructs the view of subsequent input fields.
4. Save the contact to the device database.

#### **1. Contacts Flow**

This Flow interacts with the default Google Contacts app available on Android emulators. Create a YAML file in your testing directory and use the following code to define the Flow:

```yaml
# contacts.yaml
appId: com.android.contacts
---
- launchApp

# Start the creation process
- tapOn: "Create new contact"

# Maestro generates a realistic first name automatically
- tapOn: "First name"
- inputRandomPersonName

- tapOn: "Last name"
- inputRandomPersonName

- tapOn: "Phone"
- inputRandomNumber:
    length: 10

# The keyboard often covers the 'Email' field. 
# We use 'back' to dismiss it safely.
- back

- tapOn: "Email"
- inputRandomEmail

# Finalize the contact
- tapOn: "Save"
```

The above Flow automates the contact creation, but it is important to understand how it was structured for those starting with Maestro:

* By using `inputRandomPersonName` and `inputRandomEmail`, you avoid duplicate contact errors that would occur if you used hardcoded strings. This makes the test repeatable without needing a manual cleanup after every run.
* One common cause of flaky tests on Android is a soft keyboard covering the next button you need to press. Using the `back` command is a reliable way to hide the keyboard and bring the rest of the form back into view.
* Since system apps are updated by Google, their resource IDs can change. Targeting stable accessibility labels like `"First name"` or `"Save"` makes your Flow more resilient to OS updates.

**2. Implementation**

Depending on your needs, you can run this automation directly or integrate it into a larger test. If you have the[ Maestro CLI](https://app.gitbook.com/o/zCVYm3M93B0sOcjR1Oj4/s/kq23kwiAeAnHkGJYMGDk/) installed and an active Android emulator running, you can execute this Flow immediately using the following command in your terminal:

```bash
maestro test contacts.yaml
```

You can also use the `contacts.yaml` as a subflow. In this case, if your app needs to ensure a contact exists before performing an action (like "Invite a Friend"), you can call this file as a subflow from your main test:

```yaml
# invite_friend_test.yaml
appId: com.your.app
---
- launchApp
# Ensure a contact is present in the OS before testing invites
- runFlow: contacts.yaml

# Resume testing your own app
- launchApp
- tapOn: "Invite Friends"
- assertVisible: "Invite"
```

#### Related content

Explore these pages to learn more about the automation patterns used in this example:

* [inputText](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/inputtext): See all available random data generators, including addresses and email.
* [back](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/back): Understand how to use system navigation to handle dialogs and keyboards.

