# Logging

Maestro supports logging to the console via `console.log`.

{% hint style="info" %}
Note that logging with multiple arguments is not supported. Running `console.log('My variable is', variable)` will only output `My variable is`.
{% endhint %}

#### Logging in evalScript

If you want to log something inline you can use `evalScript` to output it to the console without having to create a separate file:

```yaml
- evalScript: ${console.log('Hello from Javascript')}
```

{% content-ref url="../../api-reference/commands/evalscript.md" %}
[evalscript.md](../../api-reference/commands/evalscript.md)
{% endcontent-ref %}

#### Logging in a separate Javascript file

```yaml
- runScript: script.js
```

```javascript
// script.js

const myVar = 'foo';
console.log(myVar); // outputs 'foo'
consolel.log(`myVar is ${myVar}`) // outputs 'myVar is foo'
```

{% content-ref url="../../api-reference/commands/runscript.md" %}
[runscript.md](../../api-reference/commands/runscript.md)
{% endcontent-ref %}
