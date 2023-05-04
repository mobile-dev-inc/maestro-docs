# JavaScript

Maestro supports a minimal subset of vanilla JavaScript APIs with some purpose-built Maestro extensions. Though none of the functions that allow interaction with the OS are available (i.e. there is no access to the filesystem), those scripts offer just enough functionality to write more sophisticated conditions or make HTTP requests.

{% hint style="warning" %}
Maestro is using [Rhino](https://github.com/mozilla/rhino) under the hood to execute JavaScript, which has limited ES2015 / ES6 support. For a full list of API compatibility, please refer to this [page](https://mozilla.github.io/rhino/compat/engines.html). We therefore recommend relying on pre-ES6 APIs as much as possible to avoid any unexpected errors.
{% endhint %}
