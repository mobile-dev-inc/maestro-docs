# assertWithAI

{% hint style="warning" %}
This is an experimental feature that uses LLM technology. All feedback is welcome.
{% endhint %}

The `assertWithAI` command uses Large Language Models to validate the visual state of an application. The command captures a screenshot of the current screen and uploads it to an LLM along with a natural language assertion. The model evaluates the screenshot and returns a boolean result indicating whether the assertion is true.

This command is intended for scenarios where standard element-based assertions are difficult or impossible to implement, such as identifying complex visual patterns or dynamic content like two-factor authentication prompts.

### Command specifications

The following table describes the fields available for the `assertWithAI` command.

| Field       | Type     | Description                                                                           |
| ----------- | -------- | ------------------------------------------------------------------------------------- |
| `assertion` | `string` | The natural language description of the expected UI state to be evaluated by the LLM. |

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

Use natural language to describe complex UI elements, such as a two-factor authentication (2FA) screen.

```yaml
- assertWithAI:
    assertion: A two-factor authentication prompt, with space for 6 digits, is visible.

```

#### Video demonstration

The following video demonstrates the command in action.

{% embed url="https://www.youtube.com/watch?v=tfawnGqEhF0" %}

### Related content

Access the [AI test analysis](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/ai-test-analysis "mention") to learn how to configure the workspace to use the AI based solutions.
