---
description: Run inline JavaScript snippets in Maestro YAML for quick tasks.
---

# evalScript

For more information regarding JavaScript, please refer to the Javascript section:

{% content-ref url="../../advanced/javascript/" %}
[javascript](../../advanced/javascript/)
{% endcontent-ref %}

For very simple computations (like the one above), creating a new file might be cumbersome. `evalScript` allows you to specify JavaScript directly in your Maestro flow.

```yaml
appId: com.example
env:
    MY_NAME: John
---
- launchApp
- evalScript: ${output.myFlow = MY_NAME.toUpperCase()}
- inputText: ${output.myFlow}
```
