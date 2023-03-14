# Network Mocking

{% hint style="warning" %}
This is an experimental feature. It is not yet supported by Maestro Cloud and breaking changes might be introduced as we work. on it.
{% endhint %}

Network Mocking feature allows you to replace part or all of the network traffic coming from your app with static predefined content **in order to get more predictable test results**.

For example, if you application loads a news feed, Network Mocking would allow you to predefine what news articles will show up exactly in what order so that you can reliably test your view elements.

### Before you start

Network Mocking is an advanced concept and requires setup before using it for the first time. The process differs based on the operating system.

{% content-ref url="setup/" %}
[setup](setup/)
{% endcontent-ref %}

### Basics

Here are key facts about Maestro Network Mocking:

* Network Mocking works on a concept of _rules_.&#x20;
* A rule describes what HTTP(s) requests to incercept and what to reply back.&#x20;
* Rules are defined in YAML files. Single YAML file can contain multiple rules.
* Rule files can be stored in a folder/subfolders and are traversed recursively.
* Network requests that did not match any rule will continue to their real destination as if there was no mocking in place.

Here is the simplest example of a rule that will match a `GET` call to `https://example.com` and will reply with `Hello Maestro` instead of the usual [https://example.com](https://example.com) page:

```yaml
- path: https://example.com     # Request URL to match. Can be a regular expression.
  method: GET                   # (optional) GET is a default method
  response:
    status: 200                 # (optional) 200 is a default value
    body: "Hello World"
```

Let's assume that this file is saved under `rules/myRule.yaml` file. Assuming that you already went through the initial [Setup](setup/), the rules can then be used in Maestro flow:

```yaml
appId: my.app
---
- mockNetwork: rules    # Points to a folder with rules
- launchApp
```

Anything past `mockNetwork` command will now rely on the mocked network responses.

### Working on Rules

It might not be very convenient to re-run the whole test each time a rule changes. To assist with development, you can use the following helper commands

#### replay

`replay` command is very similar to `mockNetwork` except that it allows to mock the network without actually running a test. This is handy in cases where you want to manually interact with the app while working on rules.

```
maestro network replay {folder with rules}
```

#### record

`record` command records all the traffic from your app and stores it as rules on a disk. Though **replays produced by the command might require some manual tweaking** in order to work (i.e. replacing undeterministic URL parameters with regular expressions), it is a great way for exploring the HTTP(s) traffic emitted by your app.

```
maestro network record {output folder to store rules in}
```
