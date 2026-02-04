---
description: Select images from the device gallery in automated tests using addMedia.
---

# Choose images from the gallery

Uploading an image or updating a profile picture is a staple feature in modern mobile apps. However, automating this process is difficult because the "Media Picker" isn't actually part of your app, it’s a system-level component that looks and behaves differently depending on the OS and the specific version of Android or iOS.

While Maestro provides the `addMedia` command to seed the device with images, the act of selecting that media requires navigating a variety of system UIs.

### The workflow

Since the media picker is an external system process, you cannot rely on your app's internal IDs. Instead, you need to target the native elements of the OS. The strategy here is to:

1. Use `addMedia` (prior to this flow) to ensure the gallery isn't empty.
2. Trigger the image picker in your app.
3. Use a series of optional taps that target known system IDs for different OS versions.
4. Fall back until a match is found.

#### **1. Reusable selection flow**

This Flow (e.g., `pick_first_image.yaml`) acts as a universal adapter. It tries to identify the first thumbnail in the gallery by cycling through common IDs used by Google and Apple across various SDK versions.

```yaml
# pick_first_image.yaml
# Requirements: Images must already exist in the device gallery
# Strategy: Attempt platform-specific selectors with 'optional: true'

appId: ${APP_ID}
---
# Step 1: Android Media Selection
# Different Android versions use different underlying file managers.
- runFlow:
    when:
      platform: Android
    commands:
      # Targets the modern Android SDK 33/34 Media Provider
      - tapOn:
          id: 'com.google.android.providers.media.module:id/icon_thumbnail'
          optional: true
      
      # Fallback for older SDK 30 (DocumentsUI) selector
      - tapOn:
          id: 'com.google.android.documentsui:id/thumbnail'
          optional: true

# Step 2: iOS Media Selection
# iOS 18 introduced new grid layouts, while older versions rely on accessibility labels.
- runFlow:
    when:
      platform: iOS
    commands:
      # Targets the new iOS 18 grid layout
      - tapOn:
          id: 'PXGGridLayout-Info'
          index: 0
          optional: true
      
      # Fallback for iOS 17 and below using an accessibility label regex
      - tapOn:
          text: 'Photo, .*'
          index: 0
          optional: true
```

In a standard Maestro test, a failed `tapOn` would stop the execution. However, because we know that an iOS 18 selector will fail on an iOS 17 device, we mark these steps as optional by setting `optional: true`.

Maestro will try each selector in sequence. As soon as it finds a match, it performs the tap and moves forward. If a selector doesn't match, it simply skips to the next one without failing the test. This allows you to write a single, robust Flow that works across a fragmented ecosystem of device versions.

#### **2. Implementation**

To use this in your main test suite, ensure you have used [`addMedia`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/addmedia) earlier in your setup to guarantee the gallery has content, then invoke the subflow once the picker is open:

```yaml
# main_test.yaml
- tapOn: "Upload Profile Picture"
- runFlow: ../partials/pick_first_image.yaml
```

### Related content

Explore the following documentation pages if you'd like to dive deeper into the commands used in this example:

* [addMedia](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/addmedia "mention"): Learn how to inject images or videos into the device gallery.
