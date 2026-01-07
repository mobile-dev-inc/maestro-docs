# What is Maestro?

Maestro is the simplest and most effective open-source UI automation framework for mobile and web. It is designed to allow developers and testers to define and automate user journeys with a level of reliability and ease that traditional tools cannot match.

<figure><img src=".gitbook/assets/twitter_continuous_v3_fast.gif" alt=""><figcaption></figcaption></figure>

Traditional testing tools often require deep instrumentation, access to app source code, and complex framework knowledge. Maestro changes this by operating at "[arm's length](get-started/how-maestro-works.md#the-arms-length-philosophy)," piloting the device through the same accessibility layer used by real users. This eliminates framework dependencies and allows you to test any app regardless of whether it was built with React Native, Flutter, or Native code.

### Why choose Maestro?

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><i class="fa-shield">:shield:</i> <strong>Built-in Tolerance</strong></td><td>Maestro embraces the instability of mobile devices by automatically handling flakiness and UI settling.</td></tr><tr><td><i class="fa-timer">:timer:</i> <strong>Zero-Wait Intelligence</strong></td><td>No more manual <code>sleep()</code> calls. Maestro automatically waits for network content and animations to load.</td></tr><tr><td><i class="fa-file">:file:</i> <strong>Declarative Syntax</strong></td><td>Tests are defined in human-readable YAML files, removing the need for deep programming knowledge.</td></tr></tbody></table>

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><i class="fa-rocket-launch">:rocket-launch:</i> <strong>Blazingly Fast Iteration</strong></td><td>Tests run without compilation. Maestro monitors your files and reruns flows instantly upon saving.</td></tr><tr><td><i class="fa-box">:box:</i> <strong>Single Binary Setup</strong></td><td>Maestro is a single tool that works anywhere, avoiding the "setup hell" associated with legacy drivers.</td></tr></tbody></table>

{% hint style="success" %}
🚀 **Running in the cloud**

Ready to wire into CI or scale up your testing? Start running your flows on [Maestro's enterprise-grade Google Cloud Platform (GCP)](https://maestro.dev/cloud) infrastructure. Check the [Cloud documentation](https://app.gitbook.com/o/zCVYm3M93B0sOcjR1Oj4/s/ky7LkNoLfvcORtXOzzBs/) to learn how to use the power of GCP.
{% endhint %}

### Maestro vs competitors&#x20;

While tools like Appium or Selenium treat testing like unit tests inspecting internal APIs, Maestro treats your app as a black box. By simulating "human thumbs on a screen," Maestro validates the complete user experience stack, including interactions with the operating system, system settings, and notifications.

### Ready to start?

Explore the core components of the Maestro ecosystem and begin your journey:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>How Maestro Works</strong></td><td> Understand the "arm's length" philosophy and accessibility-first element detection.</td><td><a href="get-started/how-maestro-works.md">how-maestro-works.md</a></td></tr><tr><td><strong>Quickstart Guide</strong></td><td>Install Maestro Studio and run your first test in under five minutes.</td><td><a href="get-started/quickstart-1/">quickstart-1</a></td></tr><tr><td><strong>Maestro Solutions</strong></td><td>Compare the Maestro CLI, Maestro Studio (IDE), and Maestro Cloud to find the right tool for your workflow.</td><td><a href="get-started/our-products/">our-products</a></td></tr><tr><td><strong>Supported Platforms</strong></td><td>View the full list of supported frameworks, including Jetpack Compose, SwiftUI, and Web.</td><td><a href="get-started/supported-platform/">supported-platform</a></td></tr></tbody></table>

