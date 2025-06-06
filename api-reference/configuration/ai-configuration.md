# AI configuration

{% hint style="info" %}
👤  **Maestro Account** required - create your account for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

Some commands, such as `assertWithAI` and `assertNoDiffWithAI`, use custom AI models, which are not built directly in Maestro CLI. Therefore, to use such commands, additional configuration is required.

{% content-ref url="../commands/assertwithai.md" %}
[assertwithai.md](../commands/assertwithai.md)
{% endcontent-ref %}

{% content-ref url="../commands/assertnodefectswithai.md" %}
[assertnodefectswithai.md](../commands/assertnodefectswithai.md)
{% endcontent-ref %}

### API key

To use this command, an API key for the LLM is required. With the latest changes, we have migrated hard-coded API calls and prompts to our cloud backend, allowing us to enhance these features dynamically without requiring new CLI releases. To set it, export the `MAESTRO_CLOUD_API_KEY` env var.

```console
export MAESTRO_CLOUD_API_KEY=rb_qikYa7g2y5LcDEwLaEDz258ykjRQW7tIaR9K8jLlz6ijqCLTNfnDla3Nd17JF2ealh8kcsYHYyg35M41obGaz85VJz4uqI1orj
```
