---
description: >-
  Use JavaScript in flows for custom logic, environment variables, HTTP
  functions and Rhino/GraalJS support.
---

# Using JavaScript in Maestro

Maestro supports a minimal subset of vanilla JavaScript APIs with some purpose-built Maestro extensions. Though none of the functions that allow interaction with the OS are available (i.e. there is no access to the filesystem, no ability to require or import libraries), those scripts offer just enough functionality to write more sophisticated conditions, perform calculations or constructions, and to make HTTP requests.

{% hint style="warning" %}
Currently, Maestro by default uses the [Rhino](https://github.com/mozilla/rhino) JavaScript runtime to execute JavaScript, which has very limited modern JavaScript support. For a full list of API compatibility, please refer to [this compatibility table](https://mozilla.github.io/rhino/compat/engines.html).
{% endhint %}

{% hint style="info" %}
Maestro also supports an alternative JavaScript runtime – [GraalJS](https://github.com/oracle/graaljs). We intend to make GraalJS the default soon and then deprecate and remove Rhino. **We recommend everyone to opt-in to use GraalJS.**

**Learn more about** [**GraalJS support**](graaljs-support.md).
{% endhint %}
