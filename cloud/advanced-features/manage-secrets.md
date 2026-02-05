---
description: >-
  Pass sensitive parameters like usernames and passwords to Maestro Cloud tests
  via environment variables using the -e CLI option.
---

# Manage secrets

Avoid storing sensitive values directly in your Flow files. Maestro allows you to pass parameters as environment variables during execution.

{% hint style="info" %}
**Maestro Cloud Plan required** Secret management via environment variables is available on the [Maestro Cloud Plan](https://maestro.dev/cloud).
{% endhint %}

### Define environment variables

You can provide environment variables using the Maestro CLI or through CI integrations like GitHub Actions.

{% tabs %}
{% tab title="Maestro CLI" %}
Use the `-e` option to pass parameters as key-value pairs:

```bash
maestro cloud \
  --api-key <YOUR_API_KEY> \
  --project-id <YOUR_PROJECT_ID> \
  -e USERNAME=$TEST_USERNAME \
  -e PASSWORD=$TEST_PASSWORD \
  <APP_FILE> <FLOW_OR_FOLDER>
```
{% endtab %}

{% tab title="GitHub Action" %}
You can provide parameters in the multiline `env` field of the GitHub Action:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MOBILE_DEV_API_KEY }}
    app-file: <path to APK or iOS Simulator build>
    env: |
        USERNAME=${{ secrets.TEST_USERNAME }}
        PASSWORD=${{ secrets.TEST_PASSWORD }}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For more information about how to use parameters and constants in your Flow, access the [documentation](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants).
{% endhint %}

### Use variables in your Flows

Once defined, reference these variables in your Flow files using the `${VARIABLE_NAME}` syntax:

```yaml
appId: com.example.app
---
- launchApp
- inputText: ${USERNAME}
- tapOn: Next
- inputText: ${PASSWORD}
- tapOn: Login
```
