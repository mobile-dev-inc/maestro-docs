---
description: >-
  How to tidy a local Android device that's been cluttered with downloads or
  addMedia runs
---

# Clean a device

Successive runs of flows that either use addMedia to import images, or that download files, can leave your device in an inconsistent state for the next run.

A member of the Maestro Slack community, [AJ Owens](https://www.linkedin.com/in/owensaj/), came up with a recipe for cleaning up thier Android emulator of leftover files by driving the Files app that's installed on every emulator.

```
appId: com.example # This won't be used
---
##### How to add example data to the device to test this flow
#- addMedia: 
#    files:
#      - maestro.png
#- openLink:
#    link: https://archive.org/download/WOLF3D-MS-DOS/WOLF3D.zip
#    label: Download Wolfenstein 3D for MS-DOS
#- assertVisible: '(WOLF3D.zip. Open|File downloaded)' # Coping with different Chrome versions
#####

- pressKey: home
- swipe:
    direction: UP
- tapOn: Files


#### Delete Images
- tapOn: Show roots
- tapOn:
    text: Images
    index: 1 # Because there's a filter on the main page
- tapOn: Pictures
- runFlow:
    when:
      visible:
        id: com.google.android.documentsui:id/icon_thumb
    commands:
      - tapOn: More options
      - tapOn: Select all
      - tapOn: Delete
      - tapOn: OK


#### Delete Downloads
- tapOn: Show roots
- tapOn: Downloads
- runFlow:
    when:
      visible:
        id: com.google.android.documentsui:id/icon_thumb
    commands:
      - tapOn: More options
      - tapOn: Select all
      - tapOn: Delete
      - tapOn: OK
```

This has been tested and works on Android API 30 through to 34.
