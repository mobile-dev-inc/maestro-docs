# AI features configuration

Some commands, such as `assertWithAI` and `assertNoDiffWithAI`, use generative
AI models, which are not built directly in Maestro CLI. Therefore, to use such
commands, additional configuration is required.

{% content-ref url="../commands/assertwithai.md" %}
[assertwithai.md](../commands/assertwithai.md)
{% endcontent-ref %}

{% content-ref url="../commands/assertnodefectswithai.md" %}
[assertnodefectswithai.md](../commands/assertnodefectswithai.md)
{% endcontent-ref %}

### Model

The default model is the latest GPT-4o.

Support for more models and providers is tracked [in this issue](https://github.com/mobile-dev-inc/maestro/issues/1957).

### API key

{% hint style="success" %}
To use these features, you must have an account on [Robin](https://www.robintest.com), the official Maestro cloud platform. Make sure to [create an account](https://signin.robintest.com/sign-up) and [**retrieve your API key**](MAESTRO_CLOUD_API_KEY) to set it up correctly by following this link:

{% endhint %}

To use this command, an API key for the LLM is required. With the latest changes, we have migrated hard-coded API calls and prompts to our cloud backend, allowing us to enhance these features dynamically without requiring new CLI releases. To set it,
export the `MAESTRO_CLOUD_API_KEY` env var.

```console
export MAESTRO_CLOUD_API_KEY=rb_qikYa7g2y5LcDEwLaEDz258ykjRQW7tIaR9K8jLlz6ijqCLTNfnDla3Nd17JF2ealh8kcsYHYyg35M41obGaz85VJz4uqI1orj
```
