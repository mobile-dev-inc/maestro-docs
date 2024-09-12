# assertNoDefectsWithAI

{% hint style="warning" %}

This is an **experimental** feature powered by LLM technology. All feedback is
welcome.

{% endhint %}

```yaml
- assertNoDefectsWithAI
```

Takes a screenshot, uploads it to an LLM with a pre-made prompt, and asks the
model if it sees any common defects in the provided screenshot.

Common defects include text and UI elements being cut off, overlapping, or not
being centered within their containers.

### When to use?

We hope for `assertNoDefectsWithAI` to be used as a "smoke test" for parts of
your app that you want to ensure that "look right".

### Demo

{% embed url="https://youtu.be/tfawnGqEhF0" %}

### Output

Output is generated in HTML and JSON formats in the folder for the individual
test run:

```
~/.maestro
└── tests
    ├── 2024-08-20_213616
    │   ├── ai-(My first flow).json
    │   ├── ai-(My second flow).json
    │   ├── ai-report-(My first flow).html
    │   ├── ai-report-(My second flow).html
```

<figure><img src="../.gitbook/assets/ai_demo.png" alt=""><figcaption></figcaption></figure>

### Configuration

{% content-ref url="../../api-reference/configuration/ai-configuration.md" %}
[ai-configuration.md](../../api-reference/configuration/ai-configuration.md)
{% endcontent-ref %}
