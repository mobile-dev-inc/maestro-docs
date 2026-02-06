---
description: >-
  Run Maestro test suites and generate reports in JUnit or HTML. Learn how to
  organize flows, run multiple tests, and control execution options.
---

# Test Suites & Reports

### Running multiple tests

#### Using a folder

Maestro can run a suite of tests that live in a folder and generate a test report at the end.

To run a suite, point `maestro test` to a folder that contains the Flows

```
maestro test myFolderWithTests/
```

Maestro will run every flow from the directory _excluding subfolders_. The command will complete successfully if and only if all the Flows have been completed successfully.

#### Using a list of flows

Maestro can run a list of tests and generate a test report at the end.

To run a list of tests, pass to `maestro test` the Flows paths to the Flows you want to run separated by spaces:

```
maestro test myFolderWithTests/test1.yaml myFolderWithTests/test2.yaml
```

Maestro will run the flow for each file provided. The command will complete successfully if and only if all the Flows have been completed successfully.

### Generating reports

To generate a report, add a `--format` parameter to a `test` command:

```
maestro test --format junit myFolderWithTests/
```

Or, if you are [running in the cloud](../cloud/run-maestro-tests-in-the-cloud.md):

```
maestro cloud --format junit myFolderWithTests/
```

Once execution completes, the report will be stored in a `report.xml` file in a JUnit-compatible format that is supported by most platforms.

#### Supported formats

* `junit` - JUnit XML format

![xml](https://github.com/depapp/maestro-docs/assets/6134774/abcd3d3d-9154-4b49-85b5-274c31997771)

* `html` - HTML format

![html](https://github.com/depapp/maestro-docs/assets/6134774/8fedda56-de5e-411d-8501-63bf3c581e90)


#### Custom properties

JUnit reports can have custom properties specified on a per-test basis. This can be useful for downstream consumers of the reports, such as Test Case Management systems, where a Maestro flow might relate to a specific test case.

This is done via a `properties` field in the flow config section, with arbitrary name/value pairs.

A test that begins:

```yaml
appId: com.example
name: Example Flow
properties:
  thing: value
---
```

will include this inside the report:

```xml
<testsuites>
  <testsuite name="Test Suite" device="Maestro_Pixel_6_API_34" tests="2" failures="0" time="1.0">
    <testcase id="Example Flow" name="Example Flow" classname="Example Flow" time="1.0" status="SUCCESS">
      <properties>
        <property name="thing" value="value"/>
      </properties>
    </testcase>
    <testcase>...
```

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
flows:
  - "**" 

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

#### Analyze

{% hint style="warning" %}
This is an **experimental** feature powered by LLM technology. All feedback is welcome.
{% endhint %}

Maestro introduces a new feature that leverages AI to analyze your end-to-end (E2E) mobile tests and provide actionable insights based on your test logs, commands, and screenshots captured during your test runs. The AI-powered analysis identifies potential issues in your app's functionality, UI, and internationalization, helping you improve app quality efficiently.

**Login Requirement:** Before you use the AI analysis feature, ensure you are logged into Maestro. Run the following command:

```bash
maestro login
```

**Analyzing your tests**: To analyze your test flows with AI, use the --analyze flag with the maestro test command:

```bash
maestro test flow-file.yaml --analyze
```

{% hint style="info" %}
While we aim for precision, please note that this is a beta release, and the results should be validated before making critical decision
{% endhint %}

This will enable AI analysis and provide a detailed report based on your test artifacts:

**Examples**

Successful Analysis

Command:

```bash
maestro test flow-file.yaml --analyze
```

Output:

```bash
🔎 Analyzing Flow(s)...

To view the report, open the following link in your browser:
file:///path/to/your/insights-report.html

Analyze support is in Beta. We would appreciate your feedback in our Slack channel: #community-chat

```

<figure><img src="../.gitbook/assets/analyze-report.png" alt=""><figcaption></figcaption></figure>

No Issues Found

If no issues are detected, you will see a message like this:

```bash
Hey, we analyzed your flow for spelling, grammar, and internationalization issues, and good news 🙌 we didn't find any issues!
```

**Disabling Notifications**

To disable the AI analysis notification, set the `MAESTRO_CLI_ANALYSIS_NOTIFICATION_DISABLED` environment variable to true before running Maestro:

```bash
export MAESTRO_CLI_ANALYSIS_NOTIFICATION_DISABLED=true
```

**Feedback**

The Analyze feature is currently in Beta. Share your feedback and suggestions in our Slack channel: [#community-chat](https://mobile-dev-inc.slack.com/archives/C083YB8N42G)
