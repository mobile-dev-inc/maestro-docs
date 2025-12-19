# Email Notifications

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

You can set up Maestro to notify you and your team when a Flow in the cloud. That's useful to easily keep track if your app is working as expected.&#x20;

In the `config.yaml` file add the list of emails that should receive the notifications:

```
# .maestro/config.yaml
notifications:
  email:
    enabled: true
    recipients:
      - john@something.com
      - alice@something.com
      ... any other emails you want to send notifications to
```

{% hint style="info" %}
Note that the `config.yaml` file should be present in the root of your workspace along with your Flows, which by default is `.maestro` if you do not explicitly pass another folder as the workspace.
{% endhint %}

When a Flow fails, you will receive an email like this:

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Receiving notifications on success

By default, emails are only sent when a failure is detected. If you want to be notified on successful runs as well, add `onSuccess: true` to your config:

```
# .maestro/config.yaml
notifications:
  email:
    enabled: true
    onSuccess: true
    recipients:
      - john@something.com
      - alice@something.com
      ... any other emails you want to send success notifications to
```

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
