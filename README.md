# Maestro documentation

Maestro is an open source framework for mobile and web UI testing. Docs include setup guides, examples, and steps to run automated tests.

{% hint style="success" %}
🚀  **Running in the cloud**

Ready to wire into CI or scale up your testing? Start running your flows on Maestro's enterprise-grade Google Cloud Platform (GCP) infrastructure: [Run Maestro tests in the cloud](https://maestro.dev/cloud) and follow the [Quickstart Guide](cloud/cloud-quickstart.md) to quickly experience the power of GCP.
{% endhint %}

{% embed url="https://vimeo.com/767721667/d972c5f08e" %}

## Why Maestro?

Maestro builds on learnings from its predecessors—Appium, Espresso, UIAutomator, XCTest, Selenium, and Playwright—and allows you to easily define and test your flows.

{% hint style="info" %}
**What are flows?** Think of flows as parts of the user journey in your app. Login, Checkout, and Add to Cart are three examples of possible flows that you can define and test using Maestro.
{% endhint %}

* Built-in tolerance to flakiness. UI elements are not always where you expect them, and screen taps do not always go through. Maestro embraces the instability of mobile applications and devices and tries to counter it.
* Built-in tolerance to delays. No need to pepper your tests with `sleep()` calls. Maestro knows that it might take time to load the content (that is, over the network) and automatically waits for it, but no longer than required.
* Blazingly fast iteration. Tests run without compilation. Maestro continuously monitors your test files and reruns them as they change.
* Declarative yet powerful syntax. Define your tests in a YAML file.
* Simple setup. Maestro is a single binary that works anywhere.

## Examples

#### Twitter (mobile)

<figure><img src=".gitbook/assets/twitter_continuous_v3_fast.gif" alt=""><figcaption></figcaption></figure>

#### Simple examples

{% tabs %}
{% tab title="Android" %}
```yaml
# flow_contacts_android.yaml

appId: com.android.contacts
---
- launchApp
- tapOn: "Create new contact"
- tapOn: "First Name"
- inputText: "John"
- tapOn: "Last Name"
- inputText: "Snow"
- tapOn: "Save"
```
{% endtab %}

{% tab title="iOS" %}
```yaml
# flow_contacts_ios.yaml

appId: com.apple.MobileAddressBook
---
- launchApp
- tapOn: "John Appleseed"
- tapOn: "Edit"
- tapOn: "Add phone"
- inputText: "123123"
- tapOn: "Done"
```
{% endtab %}

{% tab title="Web" %}
```yaml
url: https://example.com
---
- launchApp
- tapOn: More information...
- assertVisible: Further Reading
```
{% endtab %}
{% endtabs %}

## Platform Support

<table><thead><tr><th width="572">Platform</th><th align="center">Supported</th></tr></thead><tbody><tr><td><a href="platform-support/android-views.md">Android - Views</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/android-jetpack-compose.md">Android - Jetpack Compose</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/ios-uikit.md">iOS - UIKit</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/ios-swiftui.md">iOS - SwiftUI</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/react-native.md">React Native</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/flutter.md">Flutter</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/web-views.md">Web Views</a></td><td align="center">✅</td></tr><tr><td><a href="platform-support/web-desktop-browser.md">Web (Desktop Browser)</a></td><td align="center">✅</td></tr><tr><td>.NET MAUI iOS</td><td align="center">✅</td></tr><tr><td>.NET MAUI Android</td><td align="center">✅</td></tr></tbody></table>

## Resources

* Blog Post: [**Introducing: Maestro — Painless Mobile UI Automation**](https://maestro.dev/blog/introducing-maestro-painless-mobile-ui-automation)
* GitHub Repository: [**https://github.com/mobile-dev-inc/maestro**](https://github.com/mobile-dev-inc/maestro)
* Public Slack Channel: [**Join the workspace**](https://slack.maestro.dev/)



## Get Started

Get started by installing the Maestro CLI:
