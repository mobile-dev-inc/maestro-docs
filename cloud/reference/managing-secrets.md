# Managing Secrets

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

There might be cases where you don't want to store certain values in a flow file itself (i.e. user name, password, etc.). Maestro solves that by taking such parameters as [variables](managing-secrets.md#using-variables-in-your-flows).

{% tabs %}
{% tab title="Maestro CLI" %}
Pass in parameters using the `-e` option:

```
maestro cloud \
  --api-key <apiKey>
  --project-id <projectId>
  -e USERNAME=$TEST_USERNAME \
  -e PASSWORD=$TEST_PASSWORD \
  <appFile> .maestro/
```
{% endtab %}

{% tab title="Github Action" %}
Parameters are provided as multiline `env` field

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

### Using variables in your flows

Once you have defined the variables, you can refer to them in your flows:

```
appId: your.app.id
---
- launchApp
- inputText: ${USERNAME}
- tapOn: Next
- inputText: ${PASSWORD}
```
