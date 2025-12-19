# Running Flows on CI

### Running in the Cloud

The easiest way to test your flows in CI is to run your flows on Maestro's enterprise-grade hosted cloud infrastructure. Since your flows run in the cloud there's no need to configure any simulators or emulators on your end. Check out the docs to get started in less than 5 minutes:

{% content-ref url="../cloud/run-maestro-tests-in-the-cloud.md" %}
[run-maestro-tests-in-the-cloud.md](../cloud/run-maestro-tests-in-the-cloud.md)
{% endcontent-ref %}

### Alternatives

Maestro CLI can run flows on any Android device/emulator that supports ADB connections and any iOS simulator that supports Facebook's IDB. You can manually orchestrate your flow execution against any provider that supports these protocols. Just use the Maestro CLI to run your flows like you would locally.
