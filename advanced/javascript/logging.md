---
description: >-
  Log values in Maestro JavaScript scripts with console.log and evalScript for
  debugging.
---

# Logging

Maestro supports logging to the console via `console.log`.

{% hint style="info" %}
Logging with multiple arguments is not supported. Running `console.log('My variable is', variable)` will only output `My variable is`.
{% endhint %}

### Logging with `evalScript` command

If you want to log something inline you can use `evalScript` to output it to the console without having to create a separate file:

```yaml
- evalScript: ${console.log('Hello from Javascript')}
```

{% content-ref url="../../api-reference/commands/evalscript.md" %}
[evalscript.md](../../api-reference/commands/evalscript.md)
{% endcontent-ref %}

### Logging in a separate JavaScript file

```yaml
- runScript: script.js
```

{% code title="script.js" %}
```javascript
const myVar = 'foo';
console.log(myVar); // outputs 'foo'
console.log(`myVar is ${myVar}`) // outputs 'myVar is foo'
```
{% endcode %}

{% content-ref url="../../api-reference/commands/runscript.md" %}
[runscript.md](../../api-reference/commands/runscript.md)
{% endcontent-ref %}
