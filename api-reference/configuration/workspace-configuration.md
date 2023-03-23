# Workspace configuration

The following properties can be configured on the workspace as a whole as part of the workspace configuration, or global config file as you might also call it.

### Maestro configuration

* `flows`: inclusion patterns regarding what Flows to include ([docs](../../cli/test-suites-and-reports.md#controlling-what-tests-to-include)). Optional.
* `includeTags`: list of tags to include on each run ([docs](../../cli/tags.md#global-tags)). Optional.
* `excludeTags`: list of tags to exclude on each run ([docs](../../cli/tags.md#global-tags)). Optional.
* `local`:
  * `deterministicOrder`: when enabled, Flows will be run in alphabetical order ([docs](../../cli/test-suites-and-reports.md#deterministic-ordering)). Optional.

### Maestro Cloud configuration

There are other workspace configuration options available that relate to Maestro Cloud which are not outlined here. Please refer to the [Maestro Cloud documentation](https://cloud.mobile.dev/) for more information.

```yaml
# .maestro/config.yaml

# Maestro config
flows:
  - "subFolder/*"
includeTags:
  - tagNameToInclude
excludeTags:
  - tagNameToExclude
local:
  deterministicOrder: true
```

