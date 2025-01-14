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

Your recording will then be available in the same directory as the test flow.



To give a startRecording a label, or mark as optional, you can use the long form of the command:

```
- startRecording:
    path: 'logging_in'
    label: 'Begin collecting test evidence'
    optional: true
    
```



To stop a recording in progress, use the `stopRecording` command.

{% content-ref url="stoprecording.md" %}
[stoprecording.md](stoprecording.md)
{% endcontent-ref %}

