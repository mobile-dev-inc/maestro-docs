# Slack Notifications

{% hint style="info" %}
Native Slack integration coming soon
{% endhint %}

You can set up Robin to notify you and your team when a Flow fails. That's useful to easily keep track if your app is working as expected.&#x20;

At this moment, we only support sending emails to Slack, but we are working on a more rich Slack integration. In order to get messages posted to a channel in your workspace, please follow these steps:

1. Configure your Slack channel to allow posting messages via email ([docs](https://slack.com/help/articles/206819278-Send-emails-to-Slack#h_01F4WDZG8RTCTNAMR4KJ7D419V))
2. Customize the integration:\
   Email Name: `Robin Notification`\
   Email Icon: [Download icon here](https://storage.googleapis.com/mobile.dev/Robin.png)

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

1. Update your `config.yaml` with the following to ensure emails are sent to your channel:

```
# .maestro/config.yaml
notifications:
  email:
    enabled: true
    recipients:
      - emailaddresstoyourchannel@slack.com
      ... any other emails you want to send notifications to
```

{% hint style="info" %}
Note that the `config.yaml` file should be present in the root of your workspace along with your Flows, which by default is `.maestro` if you do not explicitly pass another folder as the workspace.
{% endhint %}

4. That's it! When a Flow fails a message will be posted in your channel.

### Receiving notifications on success

By default, emails are only sent when a failure is detected. If you want to be notified on successful runs as well, add `onSuccess: true` to your config:

```
# .maestro/config.yaml
notifications:
  email:
    enabled: true
    onSuccess: true
    recipients:
      - emailaddresstoyourchannel@slack.com
      ... any other emails you want to send success notifications to
```
