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

### Configuration

#### Model

The default model is the latest GPT-4o.

You can configure the model to use with the `MAESTRO_CLI_AI_MODEL` env var, for example:

```console
export MAESTRO_CLI_AI_MODEL=claude-3-5-sonnet-20240620
```

Currently supported:
– GPT family of models from OpenAI
- Claude family of models from Anthropic

Support for more models and providers is tracked [in this issue](https://github.com/mobile-dev-inc/maestro/issues/1957).

#### API key

To use this command, an API key for the LLM service is required. To set it, export the
`MAESTRO_CLI_AI_KEY` env var.

For example, to set the key for OpenAI:

```console
export MAESTRO_CLI_AI_KEY=sk-4NXxdLXY4H9DZW0Vpf4lT3HuBaFJoz1zoL21eLoLRKlyXd69
```

or for Anthropic:

```console
export MAESTRO_CLI_AI_KEY=sk-ant-api03-U9vWi8GDrxRAvA2RL2RMCImYCQr8BFCbNOq2woeRXLNz2Iy4PbY1X2137leSm92mitI7F9IwxKIrXtXgTIzj7A-2AvgbwAA
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
