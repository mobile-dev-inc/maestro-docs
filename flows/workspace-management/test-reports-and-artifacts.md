---
description: Generate test reports, screenshots, and logs for debugging and CI integration.
---

# Test reports and artifacts

Once your tests have finished executing, Maestro provides structured feedback through reports and visual artifacts, like screenshots and screen recordings. These files are essential for debugging failures locally and integrating test results into your CI/CD pipelines.

### Output directory

Maestro automatically stores screenshots, logs, and metadata for every session. By default, these are stored in a specific folder depending on your operating system:

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

#### Maestro Cloud metadata in test reports

When you generate a report for tests executed on [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/readme), Maestro adds properties that link each result back to the Cloud dashboard. You don't need to configure anything; they are added to the report automatically.

| Property         | Element       | Description                                             |
|------------------|---------------|---------------------------------------------------------|
| `cloud.uploadId` | `<testsuite>` | The ID of the upload that produced this suite.          |
| `cloud.url`      | `<testsuite>` | Link to the upload in the Maestro Cloud dashboard.      |
| `cloud.runId`    | `<testcase>`  | The ID of the individual Flow run.                      |
| `cloud.runUrl`   | `<testcase>`  | Link to that Flow's run in the Maestro Cloud dashboard. |

```xml
<?xml version='1.0' encoding='UTF-8'?>
<testsuite name="Test Suite" tests="1" failures="0" time="27.521" timestamp="2026-07-27T10:54:35">
  <properties>
    <property name="cloud.uploadId" value="mupload_01kyhfysy0ecrbjt1t6n0p8bgm"/>
    <property name="cloud.url" value="https://app.maestro.dev/.../upload/mupload_01kyhfysy0ecrbjt1t6n0p8bgm"/>
  </properties>
  <testcase id="Login Flow" name="Login Flow" classname="Login Flow" time="27.406" timestamp="2026-07-27T10:54:35" status="SUCCESS">
    <properties>
      <property name="cloud.runId" value="run_01kyhfysykehzbz8x1ztx0w53k"/>
      <property name="cloud.runUrl" value="https://app.maestro.dev/.../flow/run_01kyhfysykehzbz8x1ztx0w53k"/>
    </properties>
  </testcase>
</testsuite>
```

This extra data has two primary uses:

* Most CI report viewers surface `<property>` values on the test detail page, which gives you a direct jump from a failing test in CI to its screenshots and logs in Cloud.
* An agent using the Maestro MCP can use this report as key information to investigate failures

HTML reports contain the same information to hyperlink to the suite and to each Flow run.

These properties are only present when the tests executed on Maestro Cloud. A local `maestro test` session has no Cloud counterpart, so they are omitted rather than left blank.

#### Timestamps and durations

Both report formats record when execution started and how long it took:

* The `timestamp` attribute is populated for local sessions as well as Maestro Cloud, in the local timezone, and is truncated to whole seconds so that strict JUnit XSD validators and CI importers accept it.
* The suite-level `time` for a local session is the wall-clock time elapsed across the session, not the sum of the individual Flow durations.
* HTML reports render start times in a human-readable form rather than as raw epoch or ISO-8601 values.

#### What's inside the Artifact Folder?

Each session gets a timestamped folder inside the output directory, holding the log for the session as a whole. On iOS it also holds the raw XCTest runner log, which each Flow copies into its own folder as `logs/device-xctest.log` when it finishes. Each Flow then gets its own folder inside that, named after the Flow. Sharded sessions add a `-shard-N` suffix, and a numeric suffix is added if two Flows would otherwise collide. Every Flow folder is a self-contained bundle:

```
<output-directory>/2026-07-31_173617/    # session
├── maestro.log                          # log for the whole session
├── xctest_runner_2026-07-31_173620.log  # iOS only: raw XCTest runner log
└── login_flow/                          # one folder per test
    ├── manifest.json                    # index of every artifact in this folder
    ├── commands.json                    # one entry per executed step
    ├── logs/
    │   ├── maestro.log                  # log scoped to this Flow
    │   ├── device-logcat.txt            # Android: device log
    │   ├── device-simulator.log         # iOS: device log
    │   ├── device-xctest.log            # iOS: copy of the session XCTest log
    │   ├── crash-report.txt             # if the app under test crashed
    │   └── anr-report.txt               # Android only: if the app stopped responding
    ├── screenshots/                     # step screenshots
    ├── screen-hierarchy/                # view hierarchy JSON on failing steps
    ├── takeScreenshot/                  # your takeScreenshot output
    ├── startRecording/                  # your startRecording output
    └── ai-analysis/                     # screenshots analyzed by AI commands
```

| Entry                  | Contents                                                                                                                                                                                     |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `manifest.json`        | An index of everything in the folder. Each entry gives a `kind`, a `format`, and a `relativePath`, plus `sizeBytes` for a single file or `count` for a folder of them. Read this rather than scanning the directory — it is the documented contract, and it carries a `$schema` you can validate against. |
| `commands.json`        | A JSON array with one entry per executed step, in order. Each carries the command, its `status`, `duration`, `sequenceNumber`, and any error, plus an `artifacts` list naming the files that step produced. This is where per-step attribution lives; the manifest does not carry it. A retried or repeated step appears once per attempt, and Maestro's own implicit setup steps appear alongside the ones you wrote. |
| `logs/`                | `maestro.log` scoped to this Flow, plus the device logs, whose filenames depend on the platform: Android writes `device-logcat.txt`, iOS writes `device-simulator.log` and `device-xctest.log`. Each device log's `metadata.source` in the manifest names the stream it came from — `emulator`, `simulator`, or `xctest`. A crash lands here as `crash-report.txt` on both platforms, though its contents differ: Android writes the stack trace taken from logcat, while iOS copies the simulator's `.ips` crash report verbatim, so that file holds JSON despite the `.txt` extension. On Android an ANR also lands, as `anr-report.txt`. Both are collected when the Flow ends, cover only the app under test, and only report an event from that Flow's own run, so there is at most one of each per Flow. |
| `screenshots/`         | Step screenshots, named `step-<NNN>-<type>-<detail>.png`. In a normal `maestro test` session only the failing step is captured, so a passing Flow has no `screenshots/` folder at all.         |
| `screen-hierarchy/`    | The view hierarchy as JSON, named to match the screenshot of the same step, for working out why a selector did not match. Captured alongside the step screenshots.                             |
| `takeScreenshot/`      | Screenshots your Flow asked for with [`takeScreenshot`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/takescreenshot). Paths in that command resolve inside this folder.  |
| `startRecording/`      | Videos your Flow asked for with [`startRecording`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/startrecording). Paths in that command resolve inside this folder.       |
| `ai-analysis/`         | The screenshots that AI commands analyzed, together with the defects they reported. See [AI test analysis](ai-test-analysis.md).                                                              |

{% hint style="info" %}
The tree above shows every entry Maestro can produce, not a single session's output. Entries only appear when that session created them, so the Android and iOS device logs never sit side by side, and a passing Flow that takes no screenshots of its own gets just `manifest.json`, `commands.json`, and `logs/`.

Running with `--analyze` captures considerably more: a screenshot before every action step rather than only the failing one, a `final.png` of the screen the test ended on after any `onFlowComplete` teardown, and a `screen-recording.mp4` of the whole test.
{% endhint %}

##### Controlling output directories

The contents of your artifact folders depend on which output directory you configure and whether you use one or both CLI flags.

| Case | Feature |
| ---- | ------- |
| Neither flag specified | Maestro uses the default output directories described in the [Output directory](#output-directory) section. |
| `--test-output-dir` only | Screenshots & Video, `commands.json`, and AI Reports under this directory. The session-wide `maestro.log` stays in the default output directory; each Flow's own `logs/maestro.log` is under this one. |
| `--debug-output` only | `maestro.log`, while screenshots, video, `commands.json`, and AI Reports go to the default test output tree. |
| Both flags specified | Unless they both point to the same directory, `--debug-output` receives only `maestro.log`, and `--test-output-dir` receives screenshots, video, `commands.json`, and AI Reports. |

### Next steps

Now that you can see your results, take your debugging to the next level. Learn how to generate an automated insights reports that identifies UI and spelling bugs using [AI test analysis](ai-test-analysis.md).
