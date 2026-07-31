---
description: Start recording the screen for video documentation of test runs.
---

# startRecording

The `startRecording` command begins a screen recording of the test Flow. Use this command to collect visual evidence of your test runs, especially when debugging complex UI transitions or intermittently failing tests. The resulting video file is saved in `.mp4` format.

{% hint style="info" %}
#### Important considerations

* You must use the [`stopRecording`](stoprecording.md) command to finalize the video file.&#x20;
* The behavior and file location of recordings may differ slightly when running tests via Maestro Studio compared to the CLI.
{% endhint %}

### Parameters

To use the `startRecording`, you can provide only the file name to be saved, or you can use all the following parameters:

| Parameter  | Type    | Description                                                                                                 |
| ---------- | ------- | ----------------------------------------------------------------------------------------------------------- |
| `path`     | string  | The filename for the recording, without the extension. May include subdirectories. See [Artifact paths](#artifact-paths) for info about where it's saved. |
| `label`    | string  | **(Optional)** A descriptive label for the command step that appears in the test report.                    |
| `optional` | boolean | **(Optional)** If `true`, the command does not fail the test if it cannot be executed. Defaults to `false`. |

### Usage examples

#### Basic usage

This example uses the shorthand syntax to start a recording that will be saved as `recording.mp4`.

```yaml
appId: yourAppId
---
- launchApp
- startRecording: recording
- stopRecording
```

You need to use the [`stopRecording`](stoprecording.md) command to instruct Maestro to stop recording the device screen.

#### Custom path and labels

This example uses the expanded syntax to specify a directory, a descriptive label for the reports, and marks the command as optional to ensure the test continues even if the video engine fails to start.

```yaml
- startRecording:
    path: "recordings/user_onboarding"
    label: "Capture onboarding sequence for evidence"
    optional: true
```

### Artifact paths

Maestro writes this command's output into the `startRecording` folder of the Flow's artifact bundle. See [Layout of a Flow's artifact folder](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-reports-and-artifacts#layout-of-a-flows-artifact-folder).

The `path` must name a file, and must not attempt to escape the artifacts folder. Maestro rejects the command with an `Invalid path` error (and will fail the flow) if the value:

* names a directory rather than a file
* climbs out of the command's output folder using `..`, such as `../escape`
* is an empty string, which happens when a variable in the path resolves to `""`

An absolute path is allowed as long as it still points at the correct directory. This might be used, for example, via `maestro test --test-output-dir=/tmp/maestro123 --env OUTPUTDIR=/tmp/maestro123 ...` to compute paths that work for the environment at runtime.

A variable that was never defined does **not** fail the command. It resolves to `undefined`, and the recording is silently written to `undefined.mp4`.

If the file cannot be written (e.g. full disk or read-only destination), the Flow fails with `Cannot write startRecording output to ...`.

### Related commands

* [stoprecording.md](stoprecording.md "mention")
