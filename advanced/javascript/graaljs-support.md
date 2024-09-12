# GraalJS support

It is possible to use the [GraalJS](https://github.com/oracle/graaljs) runtime
instead of [Rhino](https://github.com/mozilla/rhino) for JavaScript evaluation.
GraalJS is fully ECMAScript 2022 compliant while Rhino only supports ECMAScript
5.

{% hint style="info %}
Right now, Rhino is the default JavaScript engine, but we intend to make GraalJS
the default soon and then deprecate and remove Rhino.

[This issue track the progress](https://github.com/mobile-dev-inc/maestro/issues/2049).
{% endhint %}

#### Enable GraalJS via flow config

{% hint style="warning" %}
This only has an effect if present in the top-level flow. It is ignored when
included in any subflows.
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
The env var will have no effect when running on Maestro Cloud. Use the flow
config above to opt into GraalJS on Maestro Cloud.
{% endhint %}

```bash
export MAESTRO_USE_GRAALJS=true
maestro test my-flow.yaml
```

### GraalJS behavior differences

There are some differences between the new `GraalJsEngine` and the current `RhinoJsEngine` implementation that are worth noting. All of the differences below and some others are documented and tested by the `GraalJsEngineTest` and `RhinoJsEngineTest` tests.

{% hint style="info" %}
**TL;DR** is that the variable scoping when using GraalJS is more consistent and
understandable.
{% endhint %}

| Rhino JS                                                                                                                                                                                                                                                                                                                            | GraalJS                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| <ul><li>Can not reuse variable names across scripts within the same Flow</li></ul><ul><li>Can reuse variable names if redeclaration lives in a subflow</li></ul><ul><li>Can access variables declared earlier in the Flow in a separate script</li></ul><ul><li><code>output</code> variable is shared across all scripts</li></ul> | <ul><li>Variables are local to each script</li></ul><ul><li><code>output</code> variable is shared across all scripts</li></ul> |

**Some examples**

|                                      | Example                                                                                                             | Rhino JS                                  | GraalJS                                                              |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- | -------------------------------------------------------------------- |
| Redeclaring variables across scripts | <pre><code>appId: com.example
---
- evalScript: ${const foo = null}
- evalScript: ${const foo = null}
</code></pre> | ❌ Variable redeclarations throw an error  | ✅ Variable names can be reused across scripts                        |
| Accessing variables across scripts   | <pre><code>appId: com.example
---
- evalScript: ${const name = 'joe'}
- assertTrue: ${name === 'joe'}
</code></pre> | ✅ Variables are accessible across scripts | ❌ Variables can't be accessed across scripts                         |
| Special character handling           | <pre><code>appId: com.example.app
env:
  FOO: \
---
- inputText: ${FOO}
</code></pre>                               | ❌ Single backslash causes an exception    | ✅ Single backslash and all other special chars are handled correctly |
