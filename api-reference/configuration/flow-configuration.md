# Flow configuration

The following properties can be configured on a given Flow:

* `appId`: defines what app the Flow should start when running `launchApp` (required)
* `name`: custom name for the Flow if you don't want to use the filename (optional)
* `tags`: list of tags that this Flow is part of. More information regarding tags can be found [here](../../cli/tags.md). (optional)
* `env`: map of environment variables that should be made available for this Flow

```yaml
# flow.yaml
appId: my.app
name: Custom Flow name
tags:
  - tag-build
  - pull-request
env:
    USERNAME: user@example.com
    PASSWORD: 123
---
- launchApp
```

