# Android contacts flow automation

{% embed url="https://player.vimeo.com/video/779079600?h=0b1fec8f26" %}

This flow demonstrates how Maestro can automate saving a contact with name, phone number & email of a person.

Some notable interactions in this Flow:

1. Clicking on any element using: tapOn
2. Random data input using: inputRandomPersonName,inputRandomNumber & inputRandomEmail
3. Android back navigation using: back

## **Flow File**

{% code title="contacts.yaml" %}
```yaml
appId: com.android.contacts
---
- launchApp
- tapOn: "Create new contact"
- tapOn: "First name"
- inputRandomPersonName
- tapOn: "Last name"
- inputRandomPersonName
- tapOn: "Phone"
- inputRandomNumber:
    length: 10
- back
- tapOn: "Email"
- inputRandomEmail
- tapOn: "Save"
```
{% endcode %}

## **How to run the flow**

1. Install maestro in your system. ([Installation instructions](../getting-started/installing-maestro/))
2. Copy the YAML flow from below in your system and save it as contacts.yaml
3. Start android emulator in your system
4. Run this command from your terminal: `maestro test contacts.yaml`
