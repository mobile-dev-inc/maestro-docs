# iOS

To integrate SDK into your iOS app, follow these simple steps:

### Step 1 - Add a Dependency

{% hint style="info" %}
Only CocoaPods projects are supported at this moment. Support for other build systems are coming soon! Reach out to us on [Slack](https://docsend.com/view/3r2sf8fvvcjxvbtk) to let us know about your use case
{% endhint %}

Assuming that you are using CocoaPods, add the following pod to your `Podfile`

```ruby
pod 'MaestroSDK'
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

Initialize the SDK as soon as your application is created. Just like with any other SDK, simply add the following to your `AppDelegate`

```swift
import UIKit
import Maestro_SDK

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MaestroSdk.setup(projectId: "YOUR_PROJECT_ID")
        
        return true
    }
    
}
```

### Next Steps

The SDK is ready to be used! Check out some of the common use cases that SDK supports:

{% content-ref url="../maestro-mock-server/" %}
[maestro-mock-server](../maestro-mock-server/)
{% endcontent-ref %}
