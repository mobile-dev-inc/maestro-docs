# Detect Maestro in your App

It's sometimes useful to be able to add logic in your app that depends that whether you are running within the context of Maestro. In order to detect Maestro, check to see whether the Maestro-specific port is open on your device:

| Platform | Maestro Port on Device |
| -------- | ---------------------- |
| iOS      | 22087                  |
| Android  | 7001                   |

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
