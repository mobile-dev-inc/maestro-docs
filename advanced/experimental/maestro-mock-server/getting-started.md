# Getting started

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

First, install the latest version of `maestro` as this functionality is available from version `1.22.0` and up.

{% content-ref url="../../../getting-started/installing-maestro/" %}
[installing-maestro](../../../getting-started/installing-maestro/)
{% endcontent-ref %}

### Setup

**Step 1 - Setup Maestro SDK**

If you haven't already, make sure to setup Maestro SDK in your project first

{% content-ref url="../maestro-sdk/" %}
[maestro-sdk](../maestro-sdk/)
{% endcontent-ref %}

**Step 2 - Replace base URL**

Then, replace your API base url with a base url provided by Maestro SDK:

{% tabs %}
{% tab title="Android" %}
```kotlin
import dev.mobile.maestro.sdk.MaestroSdk

// use baseUrl as you normally would
val baseUrl = MaestroSdk.mockServer().url("https://api.company.com")
```
{% endtab %}

{% tab title="iOS" %}
```swift
import Maestro_SDK

// use baseUrl as you normally would
let baseUrl = MaestroSdk.mockServer().url(baseUrl: "https://api.company.com")
```
{% endtab %}

{% tab title="React Native" %}
```javascript
import { mockServerUrl } from 'maestro-rn-sdk';

// use baseUrl as you normally would
async function getBaseUrl() {
  await mockServerUrl('https://api.company.com')   
}
```
{% endtab %}
{% endtabs %}

You can then use `baseUrl` as you normally would.

{% hint style="warning" %}
The URL passed in should start with `https://` and should **not** have a trailing /, as that is added by Maestro SDK automatically. You can then access your API endpoint by sending requests to `${baseUrl}${path}` - you don't need to add `/` in between.
{% endhint %}

**Step 3 - Try it out**

Build and run your app and you should start seeing events in the Maestro Mock Server UI!

### Initializing mockserver workspace

You can run `maestro mockserver init` to generate a sample rule locally that you can keep building on.
