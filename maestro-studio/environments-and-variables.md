---
description: >-
  Manage dynamic test configurations in Maestro Studio. Use Environment
  Variables and Tags to run Flows across different platforms and environments.
---

# Environments and variables

Maestro Studio allows you to manage dynamic configurations through Environments. This is essential for running the same tests across different app variants, server environments, or localized settings without hardcoding values into your Flows.

### Organize your environments

To keep your tests maintainable, it is recommended to separate your environment configurations. Common use cases for different environments include:

* **Platform Variants**: Running tests against the same app on multiple platforms with different properties, such as a unique `appId` for Android vs. iOS.
* **Host Environments**: Testing against different backends (e.g., Staging vs. Production) using different credentials or API endpoints.
* **Whitelabel Variants**: Running tests against variants of a whitelabelled application that require different test data or theme settings.

### Add environments

Environments in Maestro enable you to define two key types of configurations:

* **Environment Variables**: Key-value pairs used to inject dynamic data into your tests (e.g., `BASE_URL`, `USER_EMAIL`).
* **Configure Tags**: Specify the tags to be included and excluded when running the tests. This allows you to create specific labels used to filter which Flows are executed during a run (e.g., `smoke`, `regression`).

When you start using Maestro Studio, you have the default environment, called `None`. But, to better organize your tests, it's recommended to have environments and environment variables separated.

To add a new environment, follow these steps:

1. Open the Maestro Studio.
2. In Maestro Studio, click the gear icon.
3. On the dropdown menu, select **Environments** to open the **Environment Manager** window.

<figure><img src=".gitbook/assets/set-environment.png" alt=""><figcaption></figcaption></figure>

5. In the **Environment Manager**, click the **+ Add** button.
6. Specify the **Included** and **Excluded** tags for this environment.
7. Add your variables as **Key-Value** pairs.

{% hint style="success" %}
#### Example

Imagine you have created a set of generic Flows to be used across all available operating systems. To ensure the correct tests run for a specific platform, you can create a dedicated Android Environment:

* **Filter with Tags**: Add `Android` to **includedTags** and add `iOS` and `Web` to **excludedTags**. This ensures that only Flows applicable to Android are executed.
* **Define Variables**: Specify an `appId` variable containing the unique package name for your Android app (e.g., `com.example.android`).
{% endhint %}

<figure><img src=".gitbook/assets/set-variables.png" alt=""><figcaption></figcaption></figure>

### Using variables in your Flows

Environment variables are available throughout your Flow wherever a JavaScript expression is supported. You are not limited to a specific `env` section; you can use them directly in UI commands or logic gates.

You can use the variables as direct iputs, using `${variableName}` to inject values into text fields:

```yaml
- inputText: ${email}
```

You can also use the variables to control Flow execution based on the environment:

```yaml
- runFlow:
    when:
      true: ${APP_ID == "com.example.android"}
    commands:
      - tapOn: "Start"
```

### Next steps

To take the next step with Maestro Studio, learn how to run your tests using the Maestro Cloud solution.

If you want to deepen your understanding of how Maestro works, explore the related documentation:

* [**Parameters and constants**](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants)**:** Pass dynamic values to flows using parameters and inline constants.
* [**Test discovery and tags**](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/workspace-management/test-discovery-and-tags)**:** Organize tests with tags and control which flows run using include/exclude filters.
* [**Conditions**](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/conditions): Execute commands conditionally based on visibility, platform, or custom expressions.
