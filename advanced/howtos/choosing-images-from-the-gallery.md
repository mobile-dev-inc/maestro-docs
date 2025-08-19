---
description: Pick the first item from the camera roll in Maestro
---

# Choosing images from the gallery

Uploading an image is a common pattern for applications, but it's not trivial to test. Maestro supplies the [addMedia](../../api-reference/commands/addmedia.md) command to get the image onto the device, but selecting the image isn't trivial, especially if you want your tests to work across Android and iOS, or across OS versions.



```yaml
# Picks the first image from an already open media library picker

# Platform-specific media selection
- runFlow:
    when:
      platform: android
    commands:
      # Try Android SDK 33/34 selector first, then fall back to SDK 30 selector
      - tapOn:
          id: 'com.google.android.providers.media.module:id/icon_thumbnail'
          optional: true
      - tapOn:
          id: 'com.google.android.documentsui:id/thumbnail'
          optional: true

- runFlow:
    when:
      platform: ios
    commands:
      # Try iOS 18 selector first, then fall back to iOS 17 selector
      - tapOn:
          id: 'PXGGridLayout-Info'
          index: 0
          optional: true
      - tapOn:
          text: 'Photo, .*'
          index: 0
          optional: true
```

This fragment can be used inline, or used as a subflow (e.g. `- runFlow: pickFirstImage.yaml`).

It sets all taps as optional, since expect one to fail every time, but we can also have confidence that one of them will succeed, since mobile OSes are rather invariable once released.
