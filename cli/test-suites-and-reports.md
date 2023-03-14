# Test Suites & Reports

### Running multiple tests

Maestro can run a suite of tests and generate a test report at the end.

To run a suite, point `maestro test` to a folder that contains the flows

```
maestro test myFolderWtihTests/
```

Maestro will run every flow from the directory _excluding subfolders_. The command will complete successfully if and only if all the flows have completed successfully.

### Generating reports

To generate a report, add a `--format` parameter to a `test` command:

```
maestro test --format junit myFolderWithTests/
```

Or if you are using Maestro Cloud:

```
maestro cloud --format junit myFolderWithTests/
```

Once execution completes, the report will be stored in a `report.xml` file in a JUnit-compatible format that is supported by most platforms.

#### Supported formats

* `junit` - JUnit XML format

#### Additional options

* `--output {file}` allows to override the report filename

### Controlling what tests to include

There are multiple mechanisms to control what flows to run when running a test suite.

#### Tags

Flow tags are covered extensively in the following section

{% content-ref url="tags.md" %}
[tags.md](tags.md)
{% endcontent-ref %}

#### Inclusion Patterns

By default, when running a test suite only flows from the top level of a given directory will be executed. Consider the following folder structure:

```
workspace/
  flowA.yaml
  subFolder/
    flowB.yaml
    subSubFolder/
      flowC.yaml
```

When running a `test` or `cloud` command on a `workspace` folder, only `flowA.yaml` will be executed by default (though it is still able to refer to `subFolder/flowB.yaml` and `subFolder/subSubFolder/flowC.yaml` using [`runFlow`](../advanced/nested-flows.md) command).

This behaviour can be customised by using **inclusion** **patterns.** To do that, update your `config.yaml` (create the file if missing) as following:

```yaml
flows:
  - "*"             # the default behaviour
  - "subFolder/*"
```

In such case, **both** flowA and flowB will be included into the test suite **but not flowC**.

Tests can also be included recursively:

```yaml
flows:
  - "**"
```

In this example, all flows A, B and C will be included into the test suite.

### Deterministic ordering

{% hint style="warning" %}
We discourage usage of deterministic ordering as this will block you from parallelising test execution.
{% endhint %}

{% hint style="warning" %}
This option is not supported for Maestro Cloud tests. All tests in a suite are going to be executed in parallel regardless of this setting.
{% endhint %}

Normally, tests in a suite are executed in a non-deterministic order. In cases where a fixed order of execution is required, you can force your tests to run in **alphabetical order**. Update your `config.yaml` (or create the file if missing) to enable this behaviour:

```yaml
local:
  deterministicOrder: true
```
