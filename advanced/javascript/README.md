# JavaScript

Maestro supports a minimal subset of vanilla JavaScript APIs with some
purpose-built Maestro extensions. Though none of the functions that allow
interaction with the OS are available (i.e. there is no access to the
filesystem), those scripts offer just enough functionality to write more
sophisticated conditions or make HTTP requests.

{% hint style="warning" %}
Currently, Maestro by default uses the [Rhino](https://github.com/mozilla/rhino) JavaScript runtime to execute JavaScript, which has very limited modern JavaScript support. For a full list of API compatibility, please refer to [compatibility table](https://mozilla.github.io/rhino/compat/engines.html).
We therefore recommend relying on pre-ES6 APIs as much as possible to avoid any unexpected errors.
{% endhint %}

{% hint style="info %}
Maestro also supports an alternative JavaScript runtime –
[GraalJS](https://github.com/oracle/graaljs). We intend to make GraalJS the
default soon and then deprecate and remove Rhino. We recommend everyone to
opt-in to use GraalJS.

**Learn more about [GraalJS support](./graaljs-support.md)**.
{% endhint %}
