---
description: Generate test reports, screenshots, and logs for debugging and CI integration.
---

# Test reports and artifacts

Once your tests have finished executing, Maestro provides structured feedback through reports and visual artifacts, like screenshots and screen recordings. These files are essential for debugging failures locally and integrating test results into your CI/CD pipelines.

### Output directory

Maestro automatically stores screenshots, logs, and metadata for every run. By default, these are stored in a specific folder depending on your operating system:

* **macOS and Linux**: `~/.maestro/tests`
* **Windows**: `%userprofile%\.maestro\tests`

However, you can customize this location for better organization in your CI environment. You can set the output directory using the Maestro CLI flag or permanently in your `config.yaml`.

{% tabs %}
{% tab title="Maestro CLI" %}
```bash
maestro test --test-output-dir=build/maestro-results ./e2e
```
{% endtab %}

{% tab title="config.yaml" %}
```yaml
# config.yaml
testOutputDir: build/maestro-results
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### Priority rule

The CLI flag always overrides the `config.yaml` setting, which in turn overrides the default path.
{% endhint %}

### Generating reports

Maestro supports industry-standard formats to ensure compatibility with tools like Jenkins, GitHub Actions, and Azure DevOps, as well as most Testcase Management Systems.

{% hint style="info" %}
#### CLI-dependent

To generate reports, you must use the `--format` flag when running a test with the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/).

It is not possible to define report generation directly in the `config.yaml` file.
{% endhint %}

#### **JUnit (XML) reports**

JUnit is the standard for CI/CD integration and for test reporting. To generate a JUnit report, use the `--format junit` flag.

You can specify an output file using the `--output` flag. If omitted, Maestro will generate a `report.xml` file in your current working directory. Note that these reports are not included in the `--test-output-dir` or `--debug-output` folders.

```bash
maestro test --format junit --output build/report.xml ./e2e
```

#### **HTML reports**

HTML reports provide a human-readable summary, including screenshots of failed steps. Similar to JUnit, use the `--output` flag to define a specific destination.

For simple reports, use the `html` format. There's a more detailed report available with `html-detailed` that includes steps.

```bash
maestro test --format html --output build/report.html ./e2e
maestro test --format html-detailed --output build/detailed-report.html ./e2e
```

#### Custom properties

You can add custom metadata to your JUnit report using the `properties` field in your Flow header. These properties appear as `<property>` child elements on the `<testcase>` in the XML output.

```yaml
appId: com.example.app
name: Login Flow
properties:
    testCaseId: "TC-101"
    priority: "High"
---
- launchApp
```

#### Controlling JUnit XML attributes

Two reserved property keys let you override the `id` and `classname` attributes on the `<testcase>` element:

| Key | JUnit attribute | Default |
|-----|----------------|---------|
| `junitId` | `id` | Flow name |
| `junitClassname` | `classname` | Flow name |

By default, `id`, `name`, and `classname` are all set to the flow's `name`. Set `junitId` when you want a stable identifier independent of the display name, and `junitClassname` when your CI tooling groups or deduplicates results by class.

```yaml
appId: com.example.app
name: Login Flow
properties:
    junitId: TC-LOGIN-001
    junitClassname: com.example.tests.LoginTest
---
- launchApp
```

{% hint style="info" %}
`junitId` and `junitClassname` are reserved — they set XML attributes on the `<testcase>` element and are not emitted as `<property>` child elements. All other properties are emitted as `<property>` elements.
{% endhint %}

#### What's inside the Artifact Folder?

The contents of your artifact folders depend on which CLI flag you use. Note that `--test-output-dir` and `--debug-output` capture different sets of data:

| **Feature**         | **`--test-output-dir`** | **`--debug-output`** |
| ------------------- | ----------------------- | -------------------- |
| Screenshots & Video | Yes                     | No                   |
| `maestro.log`       | No                      | Yes                  |
| `commands-*.json`   | Yes                     | Yes                  |
| AI Reports          | Yes                     | Yes                  |

When using both flags, you must consider the following behaviour:

* **Same directory**: If both flags point to the same location, all artifacts are consolidated into that single folder.
* **Different directories**: If the flags point to different directories, the `--debug-output` directory will receive **only** the `maestro.log`, while the `--test-output-dir` will receive everything else (Screenshots, Videos, Commands JSON, and AI Reports).

### Next steps

Now that you can see your results, take your debugging to the next level. Learn how to generate an automated insights reports that identifies UI and spelling bugs using [AI test analysis](ai-test-analysis.md).
