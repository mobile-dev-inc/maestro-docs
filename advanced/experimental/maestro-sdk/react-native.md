# React Native

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

With React Native, you have 2 options of integrating Maestro SDK:

* via React Native library (explained in this page)
* via native Android and iOS libraries (explained separately for [Android](android.md) and [iOS](ios.md))

To integrate SDK into your React Native app using a React Native library, follow these simple steps:

### Step 1 - Add a Dependency

To add a Maestro SDK dependency, first run:

```bash
npm install maestro-rn-sdk
```

Afterwards, if your app supports iOS, make sure that iOS CocoaPods are updated by navigating to the iOS folder and installing them:

```bash
cd ios
pod install
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

Initialize the SDK as soon as your application is created. Simply add the following to your root `App` component:

```javascript
import { setup } from 'maestro-rn-sdk';

export default function App() {
  React.useEffect(() => {  
      (async () => {
          await setup('projectId')  
      })();
  }, []);
  
  // ... rest of your app component, as usual
}
```

### Next Steps

The SDK is ready to be used! Check out some of the common use cases that SDK supports:

{% content-ref url="../maestro-mock-server/" %}
[maestro-mock-server](../maestro-mock-server/)
{% endcontent-ref %}
