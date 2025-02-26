# Facebook signup flow automation

{% embed url="https://player.vimeo.com/video/765491505?h=21d7adf282" %}

This flow demonstrates how Maestro can automate signing up with Facebook.

Some notable interactions in this Flow:

1. Clicking on any element using: `tapOn`
2. Long pressing an element using: `longPressOn`
3. Asserting visibility of element using: `assertVisible`
4. Keyboard press using: `pressKey`
5. Random data input using: `inputRandomPersonName`, `inputRandomNumber`, `inputRandomText` & `inputRandomEmail`
6. Android back navigation using: `back`

## **Flow File**

{% code title="contacts.yaml" %}
```yaml
appId: com.facebook.katana
---
- launchApp:
    appId: "com.facebook.katana"
    clearState: true
- tapOn: "Create new Facebook account"
- assertVisible: "Join Facebook"
- tapOn: "Next"
- assertVisible: "Allow Facebook to access your contacts?"
- tapOn: "Allow"
- assertVisible: "Allow Facebook to make and manage phone calls?"
- tapOn: "Allow"
- inputRandomPersonName
- tapOn: "Last Name"
- inputRandomPersonName
- tapOn: "Next"
- assertVisible: "What's your birthday?"
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
- tapOn: "Male"
- tapOn: "Next"
- tapOn: "Sign up with email address"
- assertVisible: "Enter your email address"
- inputRandomEmail
- tapOn: "Next"
- assertVisible: "Choose a password"
- inputRandomText
- tapOn: "Next"
- tapOn: "Sign up"
```
{% endcode %}

## **How to run the flow**

{% hint style="info" %}
Note: Facebook has since added checks in their app to prevent this flow from being automated.
{% endhint %}
