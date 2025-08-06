---
description: >-
  Open links or deep links in apps or browser with Maestro, bypassing iOS
  security. Part of Maestro testing tutorial.
---

# openLink

To open a link on a device (i.e. a deep link):

```yaml
- openLink: https://example.com
```

### Auto verification of your Android Apps&#x20;

If your app shows a disambiguation dialog along with other apps that can open the web link:

&#x20;![](../../.gitbook/assets/app-disambiguation_2x.png)

You can auto-verify the web link to be opened by your app with `autoVerify` attribute:

```yaml
- openLink: 
    link: https://example.com
    autoVerify: true
```

Beyond Android version 12, web links are by default opened in the web browser. It is possible for maestro to also auto-accept agreements of Google chrome if shown with the same `autoVerify` flag.

### Opening web links in the browser for Android

It is possible with maestro to force open web links with the web browser:

```yaml
- openLink: 
    link: https://example.com
    browser: true
```



### Deeplinks and Custom Protocols

Maestro will also handle custom protocol links in the openLink command:

```
- openLink:
    link: awesomeapp://settings
```

#### iOS Security Confirmation Dialogs

On some iOS versions, the first time the app is launched via deeplink, the OS security may ask for user confirmation. Note that accepting this prompt is permanent for a Simulator, and not affected by things like clearing app state.&#x20;

<p align="center"><img src="../../.gitbook/assets/image (1).png" alt=""></p>

You may need to cater for this in your flow. Example:

```
- openLink:
    link: awesomeapp://settings
- runFlow:
    when:
      visible: 'Open in "Awesome App"'
    commands:
      - tapOn: Open
```

