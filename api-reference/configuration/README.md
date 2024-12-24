# Configuration

There are two ways to configure Maestro and [Robin](https://www.robintest.com/):

1. With a root `config.yaml` file that is present in the workspace root. Typically this would be `.maestro/config.yaml`
2. Config section for a given Flow. This is the top section in the flow file, above the `---` marker.\
   For example, you specify `appId` among with other things.

{% content-ref url="workspace-configuration.md" %}
[workspace-configuration.md](workspace-configuration.md)
{% endcontent-ref %}

{% content-ref url="flow-configuration.md" %}
[flow-configuration.md](flow-configuration.md)
{% endcontent-ref %}
