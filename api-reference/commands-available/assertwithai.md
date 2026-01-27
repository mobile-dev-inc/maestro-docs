# assertWithAI

{% hint style="warning" %}
This is an experimental feature that uses LLM technology. All feedback is welcome.
{% endhint %}

The `assertWithAI` command uses Large Language Models to validate the visual state of an application. The command captures a screenshot of the current screen and uploads it to an LLM along with a natural language assertion. The model evaluates the screenshot and returns a boolean result indicating whether the assertion is true.

This command is intended for scenarios where standard element-based assertions are difficult or impossible to implement, such as identifying complex visual patterns or dynamic content like two-factor authentication prompts.

### Command specifications

The following table describes the fields available for the `assertWithAI` command.

<table><thead><tr><th width="119.77777099609375">Field</th><th width="92.33331298828125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>assertion</code></td><td><code>string</code></td><td>The natural language description of the expected UI state to be evaluated by the LLM.</td></tr><tr><td><code>optional</code></td><td>boolean</td><td><strong>Optional.</strong>  Determines if the Flow should continue if the assertion fails. Default is <code>true</code>.</td></tr></tbody></table>

{% hint style="info" %}
Since `assertWithAI` is an experimental feature, `optional` is set to `true` by default to prevent unstable AI responses from breaking your CI/CD pipelines. If you want a failed AI assertion to stop the test, you must explicitly set `optional: false`.
{% endhint %}

### Output artifacts

The command generates detailed reports in both HTML and JSON formats. These files are stored in a timestamped subdirectory within the Maestro configuration folder.

The following structure shows the location and naming convention for these artifacts:

```
~/.maestro
└── tests
    ├── 2024-08-20_213616
    │   ├── ai-(My first flow).json
    │   ├── ai-(My second flow).json
    │   ├── ai-report-(My first flow).html
    │   ├── ai-report-(My second flow).html

```

The reports provide visual confirmation of the assertion logic applied by the model.

### Usage examples

The following examples demonstrate how to implement `assertWithAI` for different validation scenarios.

#### Basic visibility check

This example validates that specific text fields are present on the screen.

```yaml
- assertWithAI:
    assertion: Login and password text fields are visible.

```

#### Complex visual validation

Use natural language to describe complex UI elements, such as a two-factor authentication (2FA) screen. To require the test to pass, set `optional: false`, so the test fails if the assertion is false.

```yaml
- assertWithAI:
    assertion: A two-factor authentication prompt, with space for 6 digits, is visible.
    optional: false
```

#### Video demonstration

The following video demonstrates the command in action.

{% embed url="https://www.youtube.com/watch?v=tfawnGqEhF0" %}

### Related content

Access the [AI test analysis](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/ai-test-analysis "mention") to learn how to configure the workspace to use the AI based solutions.
