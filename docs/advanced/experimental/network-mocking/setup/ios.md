# iOS

To setup your iOS Simulator run this command once:

```
maestro network setup
```

What it will do:

* Add Maestro PEM certificate as a trusted CA
* Reboot the Simulator

You only need to run it once per Simulator instance.

{% hint style="warning" %}
When using Network Mocking with iOS Simulator, Maestro will update network settings on your Mac by setting Proxy to point to a local proxy server. **This will essentially block internet access for your other apps** (such as browser) while Maestro is running.

Maestro will restore those settings once it stops running.
{% endhint %}
