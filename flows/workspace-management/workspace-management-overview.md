# Workspace management overview

Moving from your first test to a full-scale automation suite requires shifting your focus from "how to write a command" to "how to design a system". A well-architected Maestro workspace ensures your tests stay fast, reliable, and easy to maintain as your application evolves.

### The anatomy of a workspace

When organizing your workspace, consider the following four pillars:

{% stepper %}
{% step %}
#### **Configuration**

A Maestro workspace is centered around the [`config.yaml`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/workspace-configuration) file, which defines global rules like your `appId`, environment variables, and platform-specific behaviors. Access the [Project configuration](project-configuration.md) guide to learn how to create and manage configuration files for your suite.&#x20;
{% endstep %}

{% step %}
#### **Architecture**

Before writing dozens of tests, you must choose a repository structure that matches your app's business logic. Whether you choose a **User Journey** or **Feature Test** model, learning how to [organize your test architecture](design-your-test-architecture/) ensures your tests remain scalable and maintainable.
{% endstep %}

{% step %}
#### **Advanced execution**

As your suite grows, you need control over how tests are discovered and executed:

* [Tags](test-discovery-and-tags.md): Categorize Flows (e.g., `smoke`, `production_ready`) to run specific subsets of tests.
* [Sequential order](sequential-execution.md): While Maestro favors isolated, non-deterministic execution, you can force a strict sequence when validating complex multi-step events.
{% endstep %}

{% step %}
#### **Analysis**

Maestro doesn't just tell you if a test passed, it provides the why:

* [Reports and artifacts](test-reports-and-artifacts.md): Generate JUnit (XML) for CI/CD pipelines or human-readable HTML reports with failure screenshots.
* [AI insights](ai-test-analysis.md): Use the `--analyze` flag to automatically detect spelling errors, layout breaks, and internationalization issues that traditional assertions might miss.
{% endstep %}
{% endstepper %}

{% hint style="success" %}
#### Best practice

Each Flow should be able to run on a completely reset device, even if you are using sequential execution.
{% endhint %}

### Next steps

If you are setting up a new repository, Maestro recommends following this path:

1. Configure your  `config.yaml` using the instructions in [Project configuration](project-configuration.md).
2. Define your folder structure based on the strategies in [design-your-test-architecture](design-your-test-architecture/ "mention").
3. Tag your critical tests to organize and filter execution as described in [test-discovery-and-tags.md](test-discovery-and-tags.md "mention").
