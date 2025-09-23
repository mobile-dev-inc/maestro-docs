---
description: >-
  Configure Maestro flows with appId, tags, env variables, and hooks like
  onFlowStart/onFlowComplete.
---

# Flow configuration

The following properties can be configured on a given Flow:

* `appId`: defines what app the Flow should start when running `launchApp` (required)
* `name`: custom name for the Flow if you don't want to use the filename (optional)
* `tags`: list of tags that this Flow is part of. More information regarding tags can be found [here](../../cli/tags.md). (optional)
* `env`: map of environment variables that should be made available for this Flow
* `onFlowStart`: This is a hook that takes a list of Maestro commands as an argument. These commands will be executed before the initiation of each flow. Typically, this hook is used to run various setup scripts.
* `onFlowComplete`: This hook accepts a list of Maestro commands that are executed upon the completion of each flow. It's important to note that these commands will run regardless of whether a particular flow has ended successfully or has encountered a failure. Typically, this hook is used to run various teardown / cleanup scripts.
* `jsEngine`: Used to override the default JavaScript engine to use another supported engine instead ([docs](../../advanced/javascript/graaljs-support.md)).
* `androidWebViewHierarchy`: Used to add Chrome DevTools aid to Maestro's default understanding of what's on screen when a webview is rendered (Android only)

{% code title="flow.yaml" %}
```yaml
appId: my.app
name: Custom Flow name
tags:
  - tag-build
  - pull-request
env:
    USERNAME: user@example.com
    PASSWORD: 123
onFlowStart:
  - runFlow: setup.yaml
  - runScript: setup.js
  - <any other command>
onFlowComplete:
  - runFlow: teardown.yaml
  - runScript: teardown.js
  - <any other command>
jsEngine: rhino
androidWebViewHierarchy: devtools
---
- launchApp
```
{% endcode %}
