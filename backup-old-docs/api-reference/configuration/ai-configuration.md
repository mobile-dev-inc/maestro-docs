# AI configuration

{% hint style="info" %}
👤 **Maestro Account** required - create your account for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

Some commands, such as `assertWithAI` and `assertNoDiffWithAI`, use custom AI models, which are not built directly in Maestro CLI. Therefore, to use such commands, additional configuration is required.

{% content-ref url="../commands/assertwithai.md" %}
[assertwithai.md](../commands/assertwithai.md)
{% endcontent-ref %}

{% content-ref url="../commands/assertnodefectswithai.md" %}
[assertnodefectswithai.md](../commands/assertnodefectswithai.md)
{% endcontent-ref %}

### Authentication

To use this command, use of an LLM is required, via the Maestro Cloud backend. This allows us to enhance these features dynamically without requiring new CLI releases. This doesn't require a paid plan.

To authenticate, either:

1. Export the `MAESTRO_CLOUD_API_KEY` env var:

```console
export MAESTRO_CLOUD_API_KEY=rb_qikYa7g2y5LcDEwLaEDz258ykjRQW7tIaR9K8jLlz6ijqCLTNfnDla3Nd17JF2ealh8kcsYHYyg35M41obGaz85VJz4uqI1orj
```

2. Run `maestro login` and authenticate your local CLI instance with Maestro Cloud. This is long-lived authentication, and won't need to be done every time.
