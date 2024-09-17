# Detect Maestro in your app

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

Depending on various variables in your testing setup, the code block above might give you a `NetworkOnMainThreadException `. Get rid of the exception by moving the boolean check to a Coroutine background thread for the `Socket` usage to work without a crash:

```kotlin
viewModel.viewModelScope.launch(Dispatchers.Default) {

     val isMaestroTestSituation = isMaestro()
     
     // If need be, update UI or take other actions on the main UI thread 
     withContext(Main) {
         // button.isVisible = isMaestroTestSituation
     }
}
```

An alternative to all of this is to use [arguments](../api-reference/commands/launchapp.md#launch-arguments) and have your app detect a particular parameter to indicate Maestro's usage, e.g. `isE2ETest`.


