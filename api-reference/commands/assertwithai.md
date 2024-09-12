# assertWithAI

{% hint style="warning" %}

This is an **experimental** feature powered by LLM technology. All feedback is
welcome.

{% endhint %}

```yaml
- assertWithAI:
    assertion: Login and password text fields are visible.
```

Takes a screenshot, uploads it to an LLM with a pre-made prompt combined with
`assertion`, and asks the model if assertion is true.

### When to use?

We hope for `assertWithAI` to be useful when it's hard (or even impossible) to
write the assertion using default assertion commands.

Asserting the presence of a two-factor authentication prompt is a good example.

<figure>
<img src="../.gitbook/assets/uber_2fa.png" alt="">
<figcaption></figcaption>
</figure>

```yaml
- assertWithAI:
    assertion: A two-factor authentication prompt, with space for 6 digits, is visible.
```

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
