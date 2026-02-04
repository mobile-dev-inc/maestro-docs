---
description: Capture a screenshot and save it to the test output directory.
---

# takeScreenshot

The `takeScreenshot` command saves a screenshot of the current screen as a PNG file.

### Parameters

The `takeScreenshot` command accepts the `path` parameter:

<table><thead><tr><th width="120">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>path</code></td><td>The file name for the screenshot, without the extension. Maestro saves the screenshot as a <code>.png</code> file. The path is relative to the Maestro workspace directory, not the flow file. By default, Maestro saves screenshots to a <code>.maestro</code> folder in your workspace. If you are using <a href="https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/">Maestro Studio overview</a>, the files are saved in the <code>.maestro/screenshots</code> folder.</td></tr></tbody></table>

### Usage examples

The following example saves a screenshot as `LoginScreen.png`.

```yaml
- takeScreenshot:
    path: LoginScreen
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
