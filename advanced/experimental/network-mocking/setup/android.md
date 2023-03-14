# Android

There are several ways to setup Network Mocking for Android devices.

### Simplest option. Add a dependency.

Add the following dependency to your project:

```groovy
debugImplementation("dev.mobile:maestro-network-proxy-android-unsafe:+")
```

This will automatically set a `networkSecurityConfig` in your AndroidManifest that will trust Maestro's certificate.

This option should work for API version 24 and higher.

{% hint style="warning" %}
This version can work for non-debug builds as well, but beware that **such builds are inherently insecure** as anyone with Maestro certificate would be able to setup a man-in-the-middle attack. Typically, that is safe for internal testing but do make sure to not publish such builds for general audience.
{% endhint %}

### Advanced. Trust the Maestro certificate.

If you are already using your own `networkSecurityConfig` or have other special needs, you can instead use Maestro's certificate directly that can be [obtained here](https://storage.googleapis.com/mobile.dev/maestro/maestro.cer).
