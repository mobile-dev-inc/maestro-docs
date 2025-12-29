# Maestro Support for GraalJS

Inside Maestro test flows, you can use the GraalJS framework to enhance interactivity with your flows and Maestro CLI, Studio, or Google Cloud Platform (GCP). This document explains Maestro's support for GraalJS.

## GraalJS

Maestro supports using the [GraalJS](https://github.com/oracle/graaljs) runtime for JavaScript evaluation, which is fully ECMAScript 2022 compliant. The previous default, [Rhino](https://github.com/mozilla/rhino), only supports ECMAScript 5.

{% hint style="info" %}
Rhino is currently the default JavaScript engine, but GraalJS is expected to become the default soon. After that, Rhino is going to be deprecated and removed. [Track progress here.](https://github.com/mobile-dev-inc/maestro/issues/2049)
{% endhint %}


### Enable GraalJS

To enable GraalJS in your flows, you can follow two paths:

#### 1. Via flow config

> **Warning:**  
> This setting only works in the top-level flow and is ignored in subflows.

```yaml
appId: com.example.app
jsEngine: graaljs
---
# The ?? operator (ES2020) is not supported by Rhino
- inputText: ${null ?? 'foo'}
```

#### 2. Via environment variable

{% hint style="warning" %}
When [running in the cloud](https://docs.maestro.dev/cloud/run-maestro-tests-in-the-cloud), use the flow config above. The environment variable isn't supported in the cloud.
{% endhint %}

```bash
export MAESTRO_USE_GRAALJS=true
maestro test my-flow.yaml
```

## Differences in Graaljs

There are notable differences between `GraalJsEngine` and `RhinoJsEngine`. Maestro documents and tests these differences.

| Rhino JS | GraalJS |
| :--- | :--- |
| - Can't reuse variable names across scripts within the same flow | - Variables are local to each script |
| - Can reuse variable names if redeclared in a subflow | - The `output` variable is shared across all scripts |
| - Can access variables declared earlier in the flow | |
| - The `output` variable is shared across all scripts | |

{% hint style="info" %}
Variable scoping with GraalJS is more predictable and isolated to each script.
{% endhint %}

## Comparison between Rhino and Graaljs

| Case | Code Sample | Rhino JS | GraalJS |
| :--- | :--- | :--- | :--- |
| **Redeclaring Variables** | `const foo = null` | ❌ **Error**: Shared scope causes redeclaration failures. | ✅ **Success**: Local scope allows variable reuse. |
| **Cross-Script Access** | `const name = 'joe'` | ✅ **Success**: Variables persist across separate scripts. | ❌ **Error**: Isolated context prevents cross-script access. |
| **Special Characters** | `env: FOO: \` | ❌ **Exception**: Single backslash triggers a parsing error. | ✅ **Success**: Correctly handles backslashes and literals. |