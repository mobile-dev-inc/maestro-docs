---
description: How to check the contents of the mobile device's clipboard using Maestro
---

# Checking clipboard contents

Maestro has [copyTextFrom](../../api-reference/commands/copytextfrom.md) and [pasteText](../../api-reference/commands/pastetext.md) commands, but they use a shim of a clipboard, not the real thing. What happens when you've got a "Copy" button in your app, and want to check that the app has put the right thing into the clipboard?

This recipe comes courtesy of [GlossGenius](https://glossgenius.com/), who had exactly that problem.

```
# Uses operating system elements available in the iOS 18 Simulator / Android API 34 Emulator
# Assumes an env is provided called EXPECTED_CONTENTS
# Ends with changing the clipboard, and an attempt to reopen the app, assuming that's where we came from

appId: ${APP_ID}
---
- pressKey: Home

- runFlow:
    when:
      platform: Android
    commands:
      - tapOn: Search # Home screen widget
      - tapOn:
          id: input
      - longPressOn:
          id: input
      - tapOn: Paste

- runFlow:
    when:
      platform: iOS
    commands:
      - pressKey: Home
      - tapOn: Search # Home screen pill
      - longPressOn:
          id: SpotlightSearchField
      - tapOn: Paste

- assertVisible: ${EXPECTED_CONTENTS}

# Clear screen and clipboard for next execution
- runFlow:
    when:
      platform: Android
    commands:
      - tapOn: Clear search box
      - inputText: Hello World
      - longPressOn:
          id: input
      - tapOn: Select all
      - tapOn: Cut

- runFlow:
    when:
      platform: iOS
    commands:
      - tapOn: Clear text
      - inputText: Hello World
      - longPressOn:
          id: SpotlightSearchField
      - tapOn: Select All
      - tapOn: Cut

- launchApp:
    stopApp: false  # Bring back to the front without relaunching

```

Usage:

```
- runFlow:
    file: ../partials/check_clipboard.yaml
    env:
      EXPECTED_CONTENTS: Maestro
```
