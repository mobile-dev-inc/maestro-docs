# Workspace configuration

The directory where all your Maestro-related configuration lives is a _Maestro
workspace_ (or just _workspace_ for short).

## Maestro configuration

The following properties can be configured on the workspace as a whole as part of the workspace configuration.

* `flows`: inclusion patterns regarding what Flows to include ([docs](../../cli/test-suites-and-reports.md#controlling-what-tests-to-include)). Optional.
* `includeTags`: list of tags to include on each run ([docs](../../cli/tags.md#global-tags)). Optional.
* `excludeTags`: list of tags to exclude on each run ([docs](../../cli/tags.md#global-tags)). Optional.

### Example

Below is an example Maestro workspace configuration file. Typically it's named
`config.yaml` and placed in the `.maestro` directory in your project's root:

```yaml
flows:
  - "subFolder/*"
includeTags:
  - tagNameToInclude
excludeTags:
  - tagNameToExclude
```

### Maestro Cloud configuration

There are other workspace configuration options available that relate to Maestro Cloud which are not outlined here. Please refer to the [Maestro Cloud documentation](https://cloud.mobile.dev/) for more information.

