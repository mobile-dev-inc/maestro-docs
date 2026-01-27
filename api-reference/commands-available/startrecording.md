# startRecording

The `startRecording` command begins a screen recording of the test Flow. Use this command to collect visual evidence of your test runs, especially when debugging complex UI transitions or intermittently failing tests. The resulting video file is saved in `.mp4` format.

{% hint style="info" %}
#### Important considerations

* You must use the [`stopRecording`](stoprecording.md) command to finalize the video file.&#x20;
* The behavior and file location of recordings may differ slightly when running tests via Maestro Studio compared to the CLI.
{% endhint %}

### Parameters

To use the `startRecording`, you can provide only the file name to be saved, or you can use all the following parameters:

<table><thead><tr><th width="115.3333740234375">Parameter</th><th width="102.111083984375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>path</code></td><td><code>string</code></td><td>Specifies the file path for the recording, relative to the Flow file's directory.</td></tr><tr><td><code>label</code></td><td><code>string</code></td><td><strong>(Optional)</strong> A descriptive label for the command step that appears in the test report.</td></tr><tr><td><code>optional</code></td><td><code>boolean</code></td><td><strong>(Optional)</strong> If <code>true</code>, the command does not fail the test if it cannot be executed. Defaults to <code>false</code>.</td></tr></tbody></table>

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

### Related commands

* [stoprecording.md](stoprecording.md "mention")
