# Android

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

To integrate SDK into your Android app, follow these simple steps:

### Step 1 - Add a Dependency

Add a Maestro SDK dependency to your `build.gradle` file:

```gradle
implementation 'dev.mobile:maestro-sdk-android:+'
```

### Step 2 - Get Maestro project id

We would need a project ID in the next step. To get a project id, you would need to sign-in into your Maestro cloud account (or create a free acount if you don't have one already) by running the following commands:

```
maestro login
```

Once you are logged in, run this command to get a project id:

```
maestro mockserver projectid
```

### Step 3 - Initialize the SDK

Initialize the SDK as soon as your application is created. Just like with any other SDK, simply override `onCreate` method in your `Application` class:

```kotlin
import android.app.Application
import dev.mobile.maestro.sdk.MaestroSdk

class MyApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        MaestroSdk.init("YOUR_MAESTRO_PROJECT_ID")
    }

}
```

### Next Steps

The SDK is ready to be used! Check out some of the common use cases that SDK supports:

{% content-ref url="../maestro-mock-server/" %}
[maestro-mock-server](../maestro-mock-server/)
{% endcontent-ref %}
