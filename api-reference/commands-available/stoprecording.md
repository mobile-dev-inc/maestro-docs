---
description: Stop the current screen recording and save the video file.
---

# stopRecording

Stops an in-progress screen recording that was previously initiated by the `startRecording` command. This command takes no arguments.

{% hint style="info" %}
`stopRecording` does not fail if no recording is in progress. If your flow starts recording conditionally, do not rely on \`stopRecording\` to fail when no recording was started.
{% endhint %}

### Usage examples

The following example shows how to stop a recording within a test Flow after an action is performed.

```yaml
appId: yourAppId
---
- launchApp
- startRecording: my_recording.mp4
- tapOn: "Login"
- stopRecording
```

### Related commands

* [startrecording.md](startrecording.md "mention")
