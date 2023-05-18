# Maestro Mock Server (deprecated)

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

### Basics

Here are key facts about Maestro Mock Server.

* Maestro Mock Server works on a concept of _rules_, that are defined in a _workspace._
* A rule describes what HTTP(s) request to incercept and what to reply back.&#x20;
* Rules are defined in JavaScript files. A single JS file can contain multiple rules.
* There must always be a root `index.js` file in the mock server workspace. From that file, other JS files can be imported defining other rules.
* Maestro Mock Server requires integrating Maestro SDK in order to send all HTTP requests to the Mock Server instead of your original API
* Network requests that did not match any rule will continue to their real destination as if there was no mocking in place.
* In order for rules to be applied, they need to be _deployed_ using `maestro mockserver deploy <path to your rules>`

Here is the simplest example of a rule that will match a `GET` call to your `/endpoint` path and will reply with `Hello Maestro` instead of the usual response:

```javascript
// .maestro/mockserver/index.js

get('/endpoint', (req, res) => {
    res.json({
        message: "Hello Maestro"
    });
});
```

### Getting started

Please follow the documentation to get up and running with Maestro Mock Server!

{% content-ref url="getting-started.md" %}
[getting-started.md](getting-started.md)
{% endcontent-ref %}
