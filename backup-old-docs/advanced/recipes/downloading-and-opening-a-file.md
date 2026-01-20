---
description: How to download a PDF in a cross-platform way in Maestro
---

# Downloading and opening a file

Opening files is relatively easy, but testing it in a way that works for all versions of all OSes takes some time to get right.

This example assumes a button titled 'Maestro PDF' which triggers a download of a PDF that contains only the text 'This is a Maestro test'. The example downloads and opens the file, asserts on its contents, then returns to the app.

```
# Navigate to test document
- tapOn: 'Maestro PDF'

# For running locally, this file might already exist on your device from last time.
# If we had an IS_CLOUD variable, we could skip this step, saving a few seconds per execution.
- tapOn:
    text: 'Download again'
    waitUntilVisible: false
    optional: true

# For Android SDK 33 in Maestro Cloud, which shows location confirmation dialog
- runFlow:
    when:
      visible: 'Choose where to download'
    commands:
      - tapOn: 'Download'

# For Android SDK 33/34 which shows the file downloaded dialog. Android SDK 30 jumps straight into the PDF.
- runFlow:
    when:
      notVisible: 'This is a Maestro test.*'
    commands:
      - assertVisible: 'File downloaded'
      - tapOn: 'Open'

- assertVisible: 'This is a Maestro test.*'

# Get back to the app
- runFlow:
    when:
      platform: android
    commands:
      - back
- runFlow:
    when:
      platform: ios
    commands:
      - tapOn: 'Done'
```
