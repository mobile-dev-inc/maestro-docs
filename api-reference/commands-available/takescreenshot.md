---
description: Capture a screenshot and save it to the test output directory.
---

# takeScreenshot

The `takeScreenshot` command saves a screenshot of the current screen as a PNG file.

### Parameters

The `takeScreenshot` command accepts the `path` parameter:

| Parameter | Description                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `path`    | The file name for the screenshot, without the extension. Maestro saves the screenshot as a `.png` file. The path is relative to the Maestro workspace directory, not the flow file. By default, Maestro saves screenshots to a `.maestro` folder in your workspace. If you are using [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/), the files are saved in the `.maestro/screenshots` folder. |
| `cropOn`  | Optional. A selector to narrow the screenshot to just an element or container that you care about. Often used with [assertScreenshot](assertscreenshot.md). For a complete list of all available selectors, see the [Selectors](https://docs.maestro.dev/api-reference/selectors) documentation.                                                                                                                  |
| `label`   | Optional. A message to display when executing the evaluation.                                                                                                                                                                                                                                                                                                                                                     |

### Usage examples

The following example saves a screenshot as `LoginScreen.png`.

```yaml
- takeScreenshot:
    path: LoginScreen
```

This next example is the same login screen, but crops to the area containing the login controls

```yaml
- takeScreenshot:
    path: LoginScreen
    cropOn:
      id: LoginFormContainer
    label: Take a screenshot of the login form
```

You can also use a shorthand syntax. The following example saves a screenshot as `MainScreen.png`.

```yaml
- takeScreenshot: MainScreen
```

{% hint style="info" %}
**Maestro CLI**

If you are using the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/), you can override the default output location with the `--test-output-dir` flag when running `maestro test` or with `testOutputDir` in your workspace config. See [Test reports and artifacts](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts) for details.
{% endhint %}

### Related content

Check the [Test reports and artifacts](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts "mention") to learn how to configure the output directory.
