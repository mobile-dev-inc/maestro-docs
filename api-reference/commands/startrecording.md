# startRecording

To start a screen recording, add the `- startRecording: name` command to your Flow like this:


```yaml
appId: yourAppId
---
- launchApp
- startRecording: recording
...
- stopRecording
...
```

Your recording will then be available in your test's directory.

{% content-ref url="stoprecording.md" %}
[stoprecording.md](stoprecording.md)
{% endcontent-ref %}
