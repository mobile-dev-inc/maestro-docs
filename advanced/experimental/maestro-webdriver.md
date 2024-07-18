# Maestro WebDriver

{% hint style="warning" %}
Note that this feature is experimental and **not** under active development
{% endhint %}

Maestro has experimental support for running flows on Web since version `1.21.0` and here you can read more on how to get started trying it out!

### Running your first web flow

It doesn't take much to get started with Maestro on web – simply replace `appId` with the website you want to launch and then write your flows as usual.

```yaml
appId: "https://maestro.mobile.dev"
---
- launchApp
- tapOn: "Ask or Search"
- inputText: "Tap On View"
- tapOn: ".*tapOn.*"
- assertVisible: "In order to tap on a view with the text \"My text\".*"
```

### Maestro Studio support

You can use the WebDriver in Studio as well according to the following steps:

1. Make sure you have no emulators/simulators running
2. Run `maestro studio`
3. When prompted to select a device, pick `Chromium Desktop Browser (Experimental)` and Studio will launch with the WebDriver
4. Studio will launch with Maestro automatically opening up `https://maestro.mobile.dev` -- in order to redirect to another page, simply execute a `- launchApp: "https://yoursite.com"` in the command executor to have Maestro redirect to the site of your choice.
5. That's it! You can now explore the full functionality of Maestro WebDriver.&#x20;

### Caveats

#### Installation

WebDriver relies on Google Chrome being installed, so make sure that Google Chrome is installed on your system - you can find official installation instructions [here](https://support.google.com/chrome/answer/95346?hl=en\&co=GENIE.Platform%3DDesktop). If you run into any weird errors, please reach out on Slack and we'll try to help you out.

If you are on Windows, please follow these steps to get started in WSL terminal:

```bash
# first, update system
sudo apt update && sudo apt -y upgrade && sudo apt -y autoremove
# download latest chrome package
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
# install Chrome
sudo apt -y install ./google-chrome-stable_current_amd64.deb
# check installed chrome version
google-chrome --version
```

#### Commands pending implementation

Note that not all Maestro commands have been fully implemented in the WebDriver yet. The following commands are pending implementation:

* Swipe
* Screen recording
* Setting location

#### Maestro Cloud support

Web flows are currently not supported on Maestro Cloud but something that we are actively exploring, so please do not hesitate to reach out in our [public Slack channel](https://docsend.com/view/3r2sf8fvvcjxvbtk).
