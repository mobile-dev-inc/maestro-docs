# Detect Maestro in your app

{% tabs %}
{% tab title="Mobile" %}
## Using launch arguments

The recommended way to check if maestro is currently running is to use [arguments](../api-reference/commands/launchapp.md#launch-arguments) and have your app detect a particular parameter to indicate Maestro's usage, e.g. `isE2ETest`.

## Checking for open ports (deprecated)

{% hint style="warning" %}
Using ports is deprecated and may stop working at any time in future maestro updates and is not supported on Robin.
{% endhint %}



It's sometimes useful to be able to add logic in your app that depends that whether you are running within the context of Maestro. In order to detect Maestro, check to see whether the Maestro-specific port is open on your device:

<table><thead><tr><th width="146">Platform</th><th>Maestro Port on Device</th></tr></thead><tbody><tr><td>iOS</td><td>22087</td></tr><tr><td>Android</td><td>7001</td></tr></tbody></table>

Here's an example of how to check for Maestro in an Android app:

```kotlin
fun isMaestro(): Boolean {
    return try {
        Socket("localhost", 7001).use { true }
    } catch(ignored: IOException) {
        false
    }
}
```

### NetworkOnMainThreadException

On Android, you may encounter a `NetworkOnMainThreadException`. This means you'll need to move the call above to a background thread. As an example:

```kotlin
CoroutineScope(Dispatchers.IO).launch {
    if (isMaestro()) {
        // Do Maestro things
        
    }
}
```
{% endtab %}

{% tab title="Web" %}
## Using JS property

Maestro defines `window.maestro` property during test execution, so you can simply check if it is defined to check whether your app is running under a Maestro test:

```javascript
if (window.maestro) {
  console.log("Maestro test is running!");
}
```
{% endtab %}
{% endtabs %}



