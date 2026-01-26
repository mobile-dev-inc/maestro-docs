# Automating Facebook Sign-Up (Android)

Automating high-security applications like Facebook provides an excellent case study for handling complex form navigation, system-level permission dialogs, and native OS components like date pickers. This example walks through the sign-up process, demonstrating how to use random data generation and precise element targeting to navigate a multi-step onboarding flow.

{% hint style="warning" %}
Social media platforms, including Facebook, implement automated bot detection and security checks (like CAPTCHAs or behavioral analysis) that may intentionally block automation flows. This example was created for educational purposes on handling complex UI patterns.
{% endhint %}

### The workflow

The sign-up process involves navigating several distinct screens, each requiring a different type of interaction. The following steps summarize the process:

1. Launch the app with a cleared state to ensure a consistent starting point.
2. Grant necessary system permissions (Contacts, Phone) to proceed.
3. Use Maestro's random generators for names, emails, and passwords to bypass static data constraints.
4. Use `longPressOn` to interact with native Android `NumberPicker` components for dates.
5. Finalize the account creation process.

{% hint style="info" %}
#### Requirements

To execute this example, you must have the Facebook app installed on your Android emulator.
{% endhint %}

#### **1. The sign-up flow**

This flow targets the Facebook Android app (`com.facebook.katana`). It uses a mix of accessibility text and resource IDs to find elements.

```yaml
# facebook.yaml
appId: com.facebook.katana
---
- launchApp:
    clearState: true  # Ensures we start at the landing page every time

- tapOn: "Create new Facebook account"
- assertVisible: "Join Facebook"
- tapOn: "Next"

# Step 1: Handling System Permission Dialogs
- assertVisible: "Allow Facebook to access your contacts?"
- tapOn: "Allow"
- assertVisible: "Allow Facebook to make and manage phone calls?"
- tapOn: "Allow"

# Step 2: Name Entry with Random Data
- inputRandomPersonName
- tapOn: "Last Name"
- inputRandomPersonName
- tapOn: "Next"

# Step 3: Interacting with the Native Date Picker
- assertVisible: "What's your birthday?"
# We use longPressOn to focus the system NumberPicker fields
- longPressOn:
    id: "android:id/numberpicker_input"
    index: 0
- inputText: "Jan"
- longPressOn:
    id: "android:id/numberpicker_input"
    index: 1
- inputText: "01"
- longPressOn:
    id: "android:id/numberpicker_input"
    index: 2
- inputText: "2000"
- pressKey: Enter
- tapOn: "Next"

# Step 4: Profile Details
- tapOn: "Male"
- tapOn: "Next"
- tapOn: "Sign up with email address"
- assertVisible: "Enter your email address"
- inputRandomEmail
- tapOn: "Next"

# Step 5: Password and Finalize
- assertVisible: "Choose a password"
- inputRandomText
- tapOn: "Next"
- tapOn: "Sign up"
```

This flow utilizes several advanced Maestro features to handle out-of-app or non-standard UI behaviors:

* The Android date picker is a system component. Standard `tapOn` or `inputText` sometimes fails to focus these correctly. By using `longPressOn` with an `index`, we ensure Maestro focuses the correct internal wheel of the picker (Month, Day, or Year).
* On modern Android versions, permission requests are blocking system dialogs. We handle these by asserting their visibility and tapping the **Allow** button immediately before moving to the next app screen.
* By adding the `clearState: true` command, it wipes the app's cache and local storage, ensuring you aren't accidentally logged into a previous account when the test starts.

#### **2. Implementation**

You can run this Flow directly to test the onboarding experience on an Android emulator. If you have the [Maestro CLI](https://app.gitbook.com/o/zCVYm3M93B0sOcjR1Oj4/s/kq23kwiAeAnHkGJYMGDk/) installed, you can run the following command in your terminal to execute the test:

```bash
maestro test facebook.yaml
```

### Related content

Explore these pages to master the interaction commands used in this example:

* [longPressOn](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/longpresson "mention"): Learn how to trigger long-press events for context menus and system pickers.
* [inputText](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/inputtext "mention"): Discover all the randomized data types Maestro can generate.
