# startRecording

The `startRecording` command begins a screen recording of the test Flow. The resulting video file is saved in the same directory as the Flow file using `.mp4` format.

### Parameters

To use the `startRecording` , you can provide only the file name to be saved, or you can use all the following parameters:

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

#### With parameters

This example uses the long-form syntax to specify a path, a label, and mark the command as optional.

```yaml
- startRecording:
    path: '/recordings/logging_in'
    label: 'Begin collecting test evidence'
    optional: true
```

### Related commands

* [stoprecording.md](stoprecording.md "mention")
