# Run your first test with the Maestro CLI

## Run your first test with the Maestro CLI

In this tutorial, you will write and run your first Maestro flow. We will automate a common user journey: creating a new contact on an Android device.

### Prerequisites

Before starting, ensure you have the following:

* **Maestro CLI**: Installed on your machine.
* **Android Studio**: Installed to manage emulators.

### Step 1: Start the Android Emulator

Maestro needs a running device to interact with. We'll use an Android Emulator for this tutorial.

1. Open **Android Studio**.
2. Go to the **Device Manager** (usually found in the `Tools` menu or on the welcome screen).
3. Launch a virtual device (e.g., Pixel 4 or similar).

> \[!NOTE] We will use the system's default Contacts app (`com.android.contacts`), which comes pre-installed on standard Android emulators. You don't need to install any external app for this tutorial.

### Step 2: Create the Flow

A "Flow" in Maestro is a YAML file that tells Maestro what to do.

1. Create a new file named `contacts.yaml` in your working directory.
2. Copy and paste the following content into the file:

```yaml
appId: com.android.contacts
---
- launchApp
- tapOn: "Create new contact"
- tapOn: "First name"
- inputRandomPersonName
- tapOn: "Last name"
- inputRandomPersonName
- tapOn: "Phone"
- inputRandomNumber:
    length: 10
- back
- tapOn: "Email"
- inputRandomEmail
- tapOn: "Save"
```

#### Understanding the Flow

* `appId`: Tells Maestro which app to test. `com.android.contacts` is the package name for the Android Contacts app.
* `launchApp`: Launches the app specified by `appId`.
* `tapOn`: Simulates a tap on the screen. Maestro finds the text (e.g., "Create new contact") and taps it.
* `inputRandomPersonName` / `inputRandomEmail`: Generates random data for realistic testing.
* `back`: Simulates pressing the system Back button (typically needed to close the keyboard or go back).

### Step 3: Run the Flow

Now, let's see Maestro in action.

1. Open your terminal.
2. Navigate to the directory where you saved `contacts.yaml`.
3. Run the following command:

```bash
maestro test contacts.yaml
```

### Outcome

Maestro will connect to your running emulator and execute the steps one by one. You should see:

1. The Contacts app opens.
2. A new contact form is opened.
3. Random names and a phone number are typed in.
4. The keyboard is dismissed (via the `back` command).
5. An email is added.
6. The contact is saved.

Congratulations! You've just automated your first mobile flow with Maestro.
