# Debug Output

### Command Failure Reason

If a command fails, failure reason will be shown in red at the end.

<figure><img src="../.gitbook/assets/231784307-53c51d7f-214f-4eb4-b9ba-9ec34380d280.png" alt=""><figcaption><p>Single Flow Run Failure</p></figcaption></figure>

<figure><img src="../.gitbook/assets/231784391-31aaf0a1-5b80-4372-a1e6-b2e6642af472 (1).png" alt=""><figcaption><p>Multiple Flow Run Failures</p></figcaption></figure>

### Screenshot On Failure

By default, a screenshot will be generated upon failure under the Maestro directory i.e for Mac it's `~/.maestro/tests/<datetime>/`

<figure><img src="../.gitbook/assets/Screenshot 2023-05-18 at 18.54.16.png" alt=""><figcaption></figcaption></figure>

### Maestro Logs

Each flow run will generate:

* A `maestro.log` file that contains Maestro related logs
* A `commands-*.json` file that contains command metadata

Located under the Maestro directory by default: `~/.maestro/tests/<datetime>/` .&#x20;

You can also configure the default path for debug output by using the `--debug-output <path>` option. Example usage:

```
maestro test --debug-output /path/to/debug/logs
```

{% hint style="info" %}
Device logs are not supported but it's something we plan to add
{% endhint %}

{% hint style="info" %}
Such data will be automatically deleted after 14 days
{% endhint %}
