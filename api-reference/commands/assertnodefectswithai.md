# assertNoDefectsWithAI

{% hint style="warning" %}

This is an **experimental** feature powered by LLM technology.

{% endhint %}

```yaml
- assertNoDefectsWithAI
```

Takes a screenshot, uploads it to an LLM with a pre-made prompt, and asks the
model if it sees any obvious defects in the provided screenshot. Common defects
include text and UI elements being cut off, overlapping, or not being centered
within their containers.

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

{% content-ref url="ai-configuration.md" %}
[ai-configuration.md](ai-configuration.md)
{% endcontent-ref %}
