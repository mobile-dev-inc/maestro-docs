# Running Flows on CI

### Robin

The easiest way to test your flows in CI is to run your flows on [Robin](https://www.robintest.com/). Since your flows run in the cloud there's no need to configure any simulators or emulators on your end. Check out the [**Robin Documentation**](../cloud/robin.md) to get started in less than 5 minutes:

{% content-ref url="../cloud/robin.md" %}
[robin.md](../cloud/robin.md)
{% endcontent-ref %}

### Alternatives

Maestro CLI can run flows on any Android device/emulator that supports ADB connections and any iOS simulator that supports Facebook's IDB. You can manually orchestrate your flow execution against any provider that supports these protocols. Just use the Maestro CLI to run your flows like you would locally.
