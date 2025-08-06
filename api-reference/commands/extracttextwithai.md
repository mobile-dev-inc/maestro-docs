---
description: >-
  Extract text from images or elements without ID using AI in Maestro and store
  in variables. For mobile and web testing automation.
---

# extractTextWithAI

{% hint style="warning" %}
This is an **experimental** feature powered by LLM technology. All feedback is welcome.
{% endhint %}

```yaml
- extractTextWithAI: CAPTCHA value
- inputText: ${aiOutput}
```

Takes a screenshot and tries to extract text value from the screen using LLM. Output is then written into `aiOutput` variable.

The name of the variable is also configurable:

```yaml
- extractTextWithAI:
    query: 'CAPTCHA value'
    outputVariable: 'theCaptchaValue'
```

For AI commands to work, AI must be configured first:

{% content-ref url="../configuration/ai-configuration.md" %}
[ai-configuration.md](../configuration/ai-configuration.md)
{% endcontent-ref %}

### When to use?

`extractTextWithAI` could be a good fit when:

* View ID or content is not known beforehand
  * Search results
* Information on the screen is presented as an image
  * Promotional banners with embedded text
  * Captcha

{% hint style="info" %}
`extractTextWithAI` is not intended to be a replacement for conventional element selectors (such as used with `tapOn`). When possible, prefer to use stable IDs or text values.
{% endhint %}

### Examples

#### Amazon Search Results

Amazon reports its search results without any distinct IDs assigned to each item. We also don't know what will show up in the results beforehand. To work around this problem we can use AI to hint us what is the label of the first product item on this page and then tap on it:

```yaml
- extractTextWithAI: Title of the first item on this page
- tapOn: ${aiOutput}
```

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

### Configuration

{% content-ref url="../configuration/ai-configuration.md" %}
[ai-configuration.md](../configuration/ai-configuration.md)
{% endcontent-ref %}





