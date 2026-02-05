---
description: >-
  Configure email notifications in config.yaml for Maestro Cloud. Default sends
  on failure only; add onSuccess for successful runs.
---

# Set email notification

Configure Maestro Cloud to send email summaries for your Flow results.

{% hint style="info" %}
**Maestro Cloud Plan required** Email notifications are available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Configure email recipients

To receive email notifications, add the `notifications` mapping to your `config.yaml` file. This file should be located in the root of your workspace (usually the `.maestro` folder).

#### Notify on failure (Default)

By default, Maestro Cloud sends emails only when a Flow fails. Add the following to your `config.yaml`:

```yaml
# .maestro/config.yaml
notifications:
  email:
    enabled: true
    recipients:
      - dev-team@example.com
      - qa-lead@example.com
```

#### Notify on success and failure

If you want to receive notifications for successful runs as well, add `onSuccess: true`:

```yaml
# .maestro/config.yaml
notifications:
  email:
    enabled: true
    onSuccess: true # Enable on sucess notification
    recipients:
      - dev-team@example.com
```

### Example email notification

When a Flow fails, recipients receive an email containing a summary of the test run and a link to the detailed report in the Maestro Dashboard.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

### Related content

Check the other notification options available when testing your app with Maestro Cloud:

* [set-slack-notification.md](set-slack-notification.md "mention")
* [configure-webhooks.md](configure-webhooks.md "mention")
