# Test Suites & Reports

### Running multiple tests

Maestro can run a suite of tests and generate a test report at the end.

To run a suite, point `maestro test` to a folder that contains the Flows

```
maestro test myFolderWithTests/
```

Maestro will run every flow from the directory _excluding subfolders_. The command will complete successfully if and only if all the Flows have been completed successfully.

### Generating reports

To generate a report, add a `--format` parameter to a `test` command:

```
maestro test --format junit myFolderWithTests/
```

Or, if you are using Maestro Cloud:

```
maestro cloud --format junit myFolderWithTests/
```

Once execution completes, the report will be stored in a `report.xml` file in a JUnit-compatible format that is supported by most platforms.

#### Supported formats

* `junit` - JUnit XML format

#### Additional options

* `--output {file}` allows to override the report filename

### Controlling what tests to include

There are multiple mechanisms to control what Flows to run when running a test suite.

#### Tags

Flow tags are covered extensively in the following section:

{% content-ref url="tags.md" %}
[tags.md](tags.md)
{% endcontent-ref %}

#### Inclusion Patterns

By default, when running a test suite, only Flows from the top level of a given directory will be executed. Consider the following folder structure:

```
workspace/
  flowA.yaml
  subFolder/
    flowB.yaml
    subSubFolder/
      flowC.yaml
```

When running a `test` or `cloud` command on a `workspace` folder, only `flowA.yaml` will be executed by default (though it is still able to refer to `subFolder/flowB.yaml` and `subFolder/subSubFolder/flowC.yaml` using [`runFlow`](../advanced/nested-flows.md) command).

This behaviour can be customised by using **inclusion** **patterns.** To do that, update your `config.yaml` (create the file if missing) as follows:

```yaml
flows:
  - "*"             # the default behaviour
  - "subFolder/*"
```

In such case, **both** flowA and flowB will be included in the test suite **but not flowC**.

Tests can also be included recursively:

```yaml
flows:
  - "**"
```

In this example, all Flows A, B, and C will be included in the test suite.

### Sequential execution

To run your Flows in a given order, you can add the following configuration to your `config.yaml` file:

```yaml
# config.yaml
executionOrder:
    continueOnFailure: false # default is true
    flowsOrder:
        - flowA
        - flowB
```

This configuration describes to Maestro the order of the Flows you want to run. The list accepts either the Flow file names (without the `.yaml` extension) or the [Flow name](https://maestro.mobile.dev/api-reference/configuration/flow-configuration).

The `continueOnFailure` flag determines whether Maestro should proceed with the execution of subsequent Flows defined in the sequence if a previous one fails. As an example: if `flowA` fails and `continueOnFailure` is `true`, `flowB` will be executed. If the flag is `false`, `flowB` won't be executed. Note that Flows that are not defined in `executionOrder` will not be impacted and will always be run after the sequential Flows, irrespective of this Flow.

{% hint style="warning" %}
Note that your Flows should **not** depend on device state and should be treated as isolated, even though they run in sequence. A good rule of thumb is to ensure that each Flow can be run on a completely reset device.
{% endhint %}

#### Configuring part of the Flows to run sequentially

For instance, if you have three Flows, `flowA`, `flowB`, and `flowC`, but you want to run only `flowA` and `flowB` sequentially, don't add `flowC` and `flowD` to the list. Maestro will run these Flows in non-deterministic ordering **after** the Flow sequence has finished executing.

### Deterministic ordering

{% hint style="danger" %}
Note that deterministic ordering has been deprecated in favour of sequential execution and will be removed in a future version.
{% endhint %}

{% hint style="warning" %}
This option is not supported for Maestro Cloud tests. All tests in a suite are going to be executed in parallel, regardless of this setting.
{% endhint %}

Normally, tests in a suite are executed in a non-deterministic order. In cases where a fixed order of execution is required, you can force your tests to run in **alphabetical order**. Update your `config.yaml` (or create the file if missing) to enable this behaviour:

```yaml
local:
  deterministicOrder: true
```
