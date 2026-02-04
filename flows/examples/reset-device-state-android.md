---
description: Clear app data and reset device state between test runs on Android.
---

# Reset device state (Android)

Successive test runs that use `addMedia` to import photos or download files can leave your Android emulator in an inconsistent state. Stale files from a previous execution can lead to false positives results, where a test succeeds only because data from a prior run was still present.

To ensure a truly clean slate, you can automate the system Files app to purge these directories before or after your test suite runs.

{% hint style="info" %}
#### **Credits**

This example was shared by [AJ Owens](https://www.linkedin.com/in/owensaj/), a member of the [Maestro Slack community](https://maestrodev.typeform.com/to/FelIEe8A?typeform-source=maestro.dev), to solve the problem of persistent media on shared emulator instances.
{% endhint %}

### The workflow

Since these files exist outside your app's sandbox, you need to interact directly with the Android Files app (the default file manager on Google APIs emulators). The logic follows a "locate and destroy" pattern:

1. Exit the app and open the Android App Drawer to launch the Files app.
2. Use the hamburger menu to jump directly to Images or Downloads.
3. Evaluate if the file manager shows that thumbnails are actually present.
4. Use the system **Select all** and **Delete** commands to clear the entire directory in one action.

#### **1. Cleanup Flow**

This Flow is designed to work on Android API 30 through 34. You can run this as a standalone Flow or call it as a subflow.

```yaml
# clean_device_android.yaml
# Strategy: Use the native Files app to remove Images and Downloads.

# Step 1: Launch the Files app
- pressKey: home
- swipe:
    direction: UP
- tapOn: Files

# Step 2: Delete images
- tapOn: Show roots      # The hamburger menu
- tapOn:
    text: Images
    index: 1             # Skips the filter chip on the main page
- tapOn: Pictures

# Step 3: Conditional cleanup
# Only proceed if thumbnails (icon_thumb) are visible.
- runFlow:
    when:
      visible:
        id: "com.google.android.documentsui:id/icon_thumb"
    commands:
      - tapOn: More options
      - tapOn: Select all
      - tapOn: Delete
      - tapOn: OK

# Step 4: Delete downloads
- tapOn: Show roots
- tapOn: Downloads

- runFlow:
    when:
      visible:
        id: "com.google.android.documentsui:id/icon_thumb"
    commands:
      - tapOn: More options
      - tapOn: Select all
      - tapOn: Delete
      - tapOn: OK
```

Interacting with a system app requires targeting resource Ids that are not part of your application’s source code. The cleanup flow is structured this way for the following reasons:

* It targets the `com.android.documentsui` package, which corresponds to the native Android file manager. This ensures that Maestro locates the correct UI elements even when your main app is minimized.
* By first checking the visibility of `id: icon_thumb`, the test executes more efficiently. If the folder is already empty, Maestro avoids searching for a **Select all** button that does not exist.
* Rather than deleting files individually, which is slow, it relies on the native **Select all** action.&#x20;

#### **2. Implementation**

Because this flow interacts with the OS, it doesn't need to be part of your app's primary navigation. You can run it once at the start of your CI pipeline to ensure a fresh environment:

```bash
maestro test clean_device_android.yaml
```

Alternatively, call it as a subflow in your main test to clear specific media after a download test completes:

```yaml
# main_test.yaml
- tapOn: "Download Report"
- assertVisible: "Report.pdf"
# Cleanup after ourselves
- runFlow: ../utils/clean_device_android.yaml
```

#### Related content

Explore these pages to learn more about the commands used to manage files and system navigation:

* [Conditions](../flow-control-and-logic/conditions.md): Review how to use the `when` parameter to make your cleanup logic skip unnecessary steps.
