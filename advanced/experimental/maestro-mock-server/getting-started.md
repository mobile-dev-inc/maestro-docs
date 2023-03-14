# Getting started

{% hint style="info" %}
Note that this is Android only for now, iOS support is coming soon!
{% endhint %}

First, install the latest version of `maestro` as this functionality is available from version `1.22.0` and up.

{% content-ref url="../../../getting-started/installing-maestro/" %}
[installing-maestro](../../../getting-started/installing-maestro/)
{% endcontent-ref %}

### Setup

Run the following to start the Maestro Mock Server:

```
maestro mockserver open
```

There, you will be presented with setup instructions walking you through how to integrate the Maestro SDK into your application. Essentially, the following steps are required:

1\) Add the following dependency to your `build.gradle` (or similar):

```
implementation 'dev.mobile:maestro-sdk-android:+'
```

\
2\) Initialize the Maestro SDK:

```
MaestroSdk.init("<project_id>")
```

Note that the project id will be prefilled in your setup instructions, but if you ever want to retrieve it you can run `maestro mockserver projectid`

3\) Then, replace your API base url with a base url provided by Maestro SDK.

```
val baseUrl = MaestroSdk.mockServer().url("https://api.company.com")
```

You can then use `baseUrl` as you normally would.

{% hint style="warning" %}
The URL passed in should start with `https://` and should **not** have a trailing /, as that is added by Maestro SDK automatically. You can then access your API endpoint by sending requests to `${baseUrl}${path}` - you don't need to add `/` in between.
{% endhint %}

4\) Build and run your app and you should start seeing events in the Maestro Mock Server UI!

### Initializing mockserver workspace

You can run `maestro mockserver init` to generate a sample rule locally that you can keep building on.
