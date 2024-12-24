# GraalJS support

It is possible to use the [GraalJS](https://github.com/oracle/graaljs) runtime instead of [Rhino](https://github.com/mozilla/rhino) for JavaScript evaluation. GraalJS is fully ECMAScript 2022 compliant while Rhino only supports ECMAScript 5.

{% hint style="info" %}
Right now, Rhino is the default JavaScript engine, but we intend to make GraalJS the default soon and then deprecate and remove Rhino.

[This issue track the progress](https://github.com/mobile-dev-inc/maestro/issues/2049).
{% endhint %}

#### Enable GraalJS via flow config

{% hint style="warning" %}
This only has an effect if present in the top-level flow. It is ignored when included in any subflows.
{% endhint %}

```yaml
appId: com.example.app
jsEngine: graaljs
---
# The ?? operator is an example of an ES2020 feature and is not supported by Rhino
- inputText: ${null ?? 'foo'}
```

#### Enable GraalJS via environment variable

{% hint style="warning" %}
The env var will have no effect when running on Robin. Use the flow config above to opt into GraalJS on Robin.
{% endhint %}

```bash
export MAESTRO_USE_GRAALJS=true
maestro test my-flow.yaml
```

### GraalJS behavior differences

There are some differences between the new `GraalJsEngine` and the current `RhinoJsEngine` implementation that are worth noting. All of the differences below and some others are documented and tested by the `GraalJsEngineTest` and `RhinoJsEngineTest` tests.

{% hint style="info" %}
**TL;DR** is that the variable scoping when using GraalJS is more consistent and understandable.
{% endhint %}

| Rhino JS                                                                                                                                                                                                                                                                                                                            | GraalJS                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| <ul><li>Can not reuse variable names across scripts within the same Flow</li></ul><ul><li>Can reuse variable names if redeclaration lives in a subflow</li></ul><ul><li>Can access variables declared earlier in the Flow in a separate script</li></ul><ul><li><code>output</code> variable is shared across all scripts</li></ul> | <ul><li>Variables are local to each script</li></ul><ul><li><code>output</code> variable is shared across all scripts</li></ul> |

**Some examples**

<table data-full-width="true"><thead><tr><th>Case</th><th width="363">Code sample</th><th>Rhino JS</th><th>GraalJS</th></tr></thead><tbody><tr><td>Redeclaring variables across scripts</td><td><pre class="language-yaml"><code class="lang-yaml">appId: com.example.example
---
- evalScript: ${const foo = null}
- evalScript: ${const foo = null}
</code></pre></td><td>❌ Variable redeclarations throw an error</td><td>✅ Variable names can be reused across scripts</td></tr><tr><td>Accessing variables across scripts</td><td><pre class="language-yaml"><code class="lang-yaml">appId: com.example.example
---
- evalScript: ${const name = 'joe'}
- evalScript: ${name === 'joe'}
</code></pre></td><td>✅ Variables are accessible across scripts</td><td>❌ Variables can't be accessed across scripts</td></tr><tr><td>Handling special characters</td><td><pre class="language-yaml"><code class="lang-yaml">appId: com.example.app
env:
  FOO: \
---
- tapOn: Username
- inputText: ${FOO}
</code></pre></td><td>❌ Single backslash causes an exception</td><td>✅ Single backslash and all other special chars are handled correctly</td></tr></tbody></table>
