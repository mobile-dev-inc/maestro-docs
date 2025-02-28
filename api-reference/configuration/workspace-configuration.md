# Workspace configuration

The directory where all your Maestro-related configuration lives is a _Maestro workspace_ (or just _workspace_ for short).

## Maestro configuration

The following properties can be configured on the workspace as a whole as part of the workspace configuration.

* `flows`: inclusion patterns regarding what Flows to include ([docs](../../cli/test-suites-and-reports.md#controlling-what-tests-to-include)). Optional.
* `includeTags`: list of tags to include on each run ([docs](../../cli/tags.md#global-tags)). Optional.
* `excludeTags`: list of tags to exclude on each run ([docs](../../cli/tags.md#global-tags)). Optional.

### Example

Below is an example Maestro workspace configuration file. Typically it's named `config.yaml` and placed in the `.maestro` directory in your project's root:

```yaml
flows:
  - "subFolder/*"
includeTags:
  - tagNameToInclude
excludeTags:
  - tagNameToExclude
```

### Robin configuration

There are other workspace configuration options available that relate to [Robin](https://www.robintest.com/) which are not outlined here. Please refer to the [Robin documentation](../../cloud/run-maestro-tests-in-the-cloud.md) for more information.

## Environment variables

| Variable name                     | Description                                                                       | Type    | Default                  | Further reading                                                      |
| --------------------------------- | --------------------------------------------------------------------------------- | ------- | ------------------------ | -------------------------------------------------------------------- |
| MAESTRO\_API\_URL                 | The URL of the Maestro API to use. Probably only useful to Mobile Inc developers. | String  | `https://api.mobile.dev` | -                                                                    |
| MAESTRO\_CLI\_AI\_KEY             | Key for external AI service used in AI operations.                                | String  | -                        | [Docs](ai-configuration.md).                                         |
| MAESTRO\_CLI\_NO\_ANALYTICS       | Disables Maestro analytics collection                                             | Boolean | `false`                  | -                                                                    |
| MAESTRO\_CLOUD\_API\_KEY          | The API key to use when communicating with Robin                                  | String  | -                        | [Robin documentation](../../cloud/run-maestro-tests-in-the-cloud.md) |
| MAESTRO\_DISABLE\_UPDATE\_CHECK   | Disable the check for newer Maestro versions when running the CLI                 | Boolean | `false`                  | -                                                                    |
| MAESTRO\_DRIVER\_STARTUP\_TIMEOUT | The maximum time to wait for a driver to start.                                   | Number  | `15000`                  | [Docs](../../advanced/configuring-maestro-driver-timeout.md)         |
| MAESTRO\_USE\_GRAALJS             | Use GraalJS instead of RhinoJS for JavaScript execution                           | Boolean | `false`                  | [Docs](../../advanced/javascript/graaljs-support.md).                |

Any other environment variables prefixed with `MAESTRO_` will be available in your Flows as JavaScript variables. See [Accessing variables from the shell](../../advanced/parameters-and-constants.md#accessing-variables-from-the-shell) for more information.
