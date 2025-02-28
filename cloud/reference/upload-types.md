# Upload Types

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

When integrating with Robin, there are three types of uploads that can be made to the platform.

#### Adhoc&#x20;

An Adhoc upload is a nomal upload that is not associated with a Pull Request or the baseline branch.

#### Baseline Commit

A Baseline Commit is an upload that is triggered from the baseline branch. These uploads are used by Robin to reference the baseline when computing whether a given Pull Request introduces a regression or not. In order to supply Robin with the most updated baseline commits, it is recommended to setup your CI to trigger an upload on every commit to your baseline branch.

#### Pull Request

A Pull Request upload should be triggered on every Pull Request against your baseline branch. Whenever this type of upload is made, Robin will report back status check to your CI (if supported) and mark checks as failed in the case of a regression. This way Robin can help you prevent regressions from being introduced into your baseline branch.
