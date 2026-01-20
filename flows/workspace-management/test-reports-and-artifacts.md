# Test reports and artifacts

Once your tests have finished executing, Maestro provides structured feedback through reports and visual artifacts, like screenshots and screen recordings. These files are essential for debugging failures locally and integrating test results into your CI/CD pipelines.

### Output directory

Maestro automatically stores screenshots, logs, and metadata for every run. By default, these are stored in a folder at `~/.maestro/`. However, you can customize this location for better organization in your CI environment.

You can set the output directory using the Maestro CLI flag or permanently in your `config.yaml`. If you are using the CLI, use the `--test-output-dir`  flag to define the output directory:

```bash
maestro test . --test-output-dir=build/maestro-results
```

You can also define the output directory directly in the `config.yaml` file:

```yaml
# config.yaml
testOutputDir: build/maestro-results
```

{% hint style="info" %}
#### Priority rule

The CLI flag always overrides the `config.yaml` setting, which in turn overrides the default `~/.maestro` path.
{% endhint %}

### Generating reports

Maestro supports industry-standard formats to ensure compatibility with tools like Jenkins, GitHub Actions, and Azure DevOps.

{% hint style="info" %}
#### CLI-dependent

To generate reports, you must use the `--format` flag when running a test with the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/).\
It is not possible to define report generation directly in the `config.yaml` file.
{% endhint %}

#### **JUnit (XML) reports**

JUnit is the standard for CI/CD integration. It allows your build tool to parse test results, track trends, and fail the build if thresholds aren't met. To generate the report using the JUnit format, use the flag

```
maestro test . --format junit
```

#### **HTML Reports**

HTML reports provide a human-readable summary, including screenshots of failed steps and detailed error messages.

```bash
maestro test . --format html
```

#### Custom properties

If you use a Test Case Management (TCM) system (like TestRail or Xray), you may need to map a Maestro Flow to a specific Test Case ID. You can add custom metadata to your JUnit report using the `properties` field in your Flow header.

{% hint style="info" %}
You can add properties only to your Flow YAML file. It is not possible to define properties in your `config.yaml` file.
{% endhint %}

In your Flow file:

```yaml
appId: com.example.app
name: Login Flow
properties:
    testCaseId: "TC-101"
    priority: "High"
---
- launchApp
```

Resulting JUnit XML:

```xml
<testcase name="Login Flow" status="SUCCESS">
  <properties>
    <property name="testCaseId" value="TC-101"/>
    <property name="priority" value="High"/>
  </properties>
</testcase>
```

#### What's Inside the Artifact Folder?

When a test run completes, the output directory contains the following assets:

| **Artifact**                 | **Description**                                                     |
| ---------------------------- | ------------------------------------------------------------------- |
| `screenshots/`               | Visual captures of the app state at the moment of a failure.        |
| `maestro.log`                | Detailed technical logs from the Maestro engine and device driver.  |
| `commands-*.json`            | Metadata for every command executed, including duration and status. |
| `report.xml` / `report.html` | The generated summary of the entire test suite.                     |

### Next Steps

Now that you can see your results, take your debugging to the next level. Learn how to generate an automated insights reports that identifies UI and spelling bugs using [AI test analysis](ai-test-analysis.md).
