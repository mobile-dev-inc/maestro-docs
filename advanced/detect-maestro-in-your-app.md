# Detect Maestro in your App

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

An alternative is to use [arguments](../api-reference/commands/launchapp.md#launch-arguments) and have your app detect a particular parameter to indicate Maestro's usage, e.g. `isE2ETest`.
