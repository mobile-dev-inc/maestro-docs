---
description: AI-powered visual testing to detect UI defects and anomalies.
---

# assertNoDefectsWithAI

{% hint style="warning" %}
This is an experimental feature that uses LLM technology. All feedback is welcome.
{% endhint %}

The `assertNoDefectsWithAI` command takes a screenshot of the current view and sends it to an LLM to analyze for common visual defects. The command checks for issues such as text or UI elements that are cut off, overlapping, or not centered correctly within their containers.

Use this command as a general smoke test to verify that UI elements in your application render as expected.

### Command specifications

The `assertNoDefectsWithAI` accepts only one parameter:

<table><thead><tr><th width="126">Parameter</th><th width="96">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>optional</code></td><td>boolean</td><td><strong>Optional.</strong> Determines if the Flow should continue if the assertion fails. Default is <code>true</code>.</td></tr></tbody></table>

{% hint style="info" %}
Since `assertNoDefectsWithAI` is an experimental feature, `optional` is set to `true` by default to prevent unstable AI responses from breaking your CI/CD pipelines. If you want a failed AI assertion to stop the test, you must explicitly set `optional: false`.
{% endhint %}

### Output

The command generates an analysis report in both `HTML` and `JSON` formats. The output files are saved in the directory for the specific test run.

```
~/.maestro
└── tests
    ├── 2024-08-20_213616
    │   ├── ai-(My first flow).json
    │   ├── ai-(My second flow).json
    │   ├── ai-report-(My first flow).html
    │   ├── ai-report-(My second flow).html
```

The HTML report provides a visual summary of the findings.

![AI analysis report showing a screenshot with highlighted defects.](https://2384395183-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fn5KVIOjVkVjYRyVWZ0yT%2Fuploads%2Fgit-blob-c2909fc1a2e650255b19d003fb4aa19d0f25f02c%2Fai_demo.png?alt=media)

### Usage examples

The following video demonstrates the command in action.

{% embed url="https://youtu.be/tfawnGqEhF0" %}

### Related content

Access the [AI test analysis](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/ai-test-analysis "mention") to learn how to configure the workspace to use the AI based solutions.
