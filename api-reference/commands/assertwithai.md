# assertWithAI

{% hint style="warning" %}

This is an **experimental** feature powered by LLM technology.

{% endhint %}

### When to use?

{% hint style="warning" %}

As all things generative AI, `assertWithAI` can be very helpful, but don't trust
it blindly.

{% endhint %}

`assertWithAI` is useful when it's hard (or even impossible) to write the
assertion using default assertion commands.

Asserting the presence of a two-factor authentication prompt is a good example.

<figure><img src="../.gitbook/assets/uber_2fa.png" alt=""><figcaption></figcaption></figure>

```yaml
- assertWithAI:
    assertion: A two-factor authentication prompt, with space for 6 digits, is visible.
```


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
