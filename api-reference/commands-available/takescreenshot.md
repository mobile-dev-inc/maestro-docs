---
description: Capture a screenshot and save it to the test output directory.
---

# takeScreenshot

The `takeScreenshot` command saves a screenshot of the current screen as a PNG file.

### Parameters

The `takeScreenshot` command accepts the `path` parameter:

| Parameter | Description                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `path`    | The filename for the screenshot, without the extension. May include subdirectories. See [Artifact paths](#artifact-paths) for info about where it's saved. |
| `cropOn`  | Optional. A selector to narrow the screenshot to just an element or container that you care about. Often used with [assertScreenshot](assertscreenshot.md). For a complete list of all available selectors, see the [Selectors](../selectors/) documentation.                                                                                                                                                     |
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

You can also group screenshots into subdirectories of the artifact folder.

```yaml
- takeScreenshot:
    path: checkout/PaymentScreen
```

### Artifact paths

Maestro writes this command's output into the `takeScreenshot` folder of the Flow's artifact bundle. See [Layout of a Flow's artifact folder](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts#layout-of-a-flows-artifact-folder).

The `path` must name a file, and must not attempt to escape the artifacts folder. Maestro rejects the command with an `Invalid path` error (and will fail the flow) if the value:

* names a directory rather than a file
* climbs out of the command's output folder using `..`, such as `../escape`
* is an empty string, which happens when a variable in the path resolves to `""`

An absolute path is allowed as long as it still points at the correct directory. This might be used, for example, via `maestro test --test-output-dir=/tmp/maestro123 --env OUTPUTDIR=/tmp/maestro123 ...` to compute paths that work for the environment at runtime.

A variable that was never defined does **not** fail the command. It resolves to `undefined`, and the screenshot is silently written to `undefined.png`.

If the file cannot be written (e.g. full disk or read-only destination), the Flow fails with `Cannot write startRecording output to ...`.

{% hint style="info" %}
**Maestro CLI**

If you are using the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/), you can override the default output location with the `--test-output-dir` flag when running `maestro test` or with `testOutputDir` in your workspace config. See [Test reports and artifacts](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts) for details.
{% endhint %}

### Related content

Check the [Test reports and artifacts](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts "mention") to learn how to configure the output directory.
