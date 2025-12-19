# Web (Desktop Browser)

<figure><img src="../.gitbook/assets/Chromium Banner (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Desktop support is currently in Beta. We would appreciate your feedback!
{% endhint %}

Maestro can test Web apps / web pages running on a desktop browser.

### Example Usage

The syntax is exactly the same as for any other Maestro test. For readability, you should specify `url` instead of an `appId` in your test file (but they're synonyms behind the scenes).

```yaml
# example.yaml

url: https://maestro.mobile.dev
---
- launchApp
- tapOn: Installing Maestro
- assertVisible: Installing the CLI
```

Then run it with:

```
maestro test example.yaml
```

{% hint style="info" %}
Maestro will spend some time downloading Chromium on the first launch. Each following test will run much faster.
{% endhint %}

### Maestro Studio

To launch Maestro Studio for Web, use the `-p web` option:

```
maestro -p web studio
```

### Other Resources

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="../api-reference/commands/" %}
[commands](../api-reference/commands/)
{% endcontent-ref %}

### Known Limitations

These features are not supported yet but should be feasible to implement if there is a common demand:

* Different browsers support (current default is Chromium)
* Different locales support (current default is en-US)
* Screen size configuration
* Flutter Web is different, in the same way Flutter Mobile is different. See the [Flutter](flutter.md) docs for how to use Semantics to make elements addressable.
