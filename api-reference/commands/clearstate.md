# clearState

Clears the application state:

```yaml
- clearState            # clears the state of the current app
- clearState: app.id    # clears the state of an arbitrary app
```

#### What is being cleared?

{% tabs %}
{% tab title="Android" %}
The outcome of the command is identical to:

```
adb shell pm clear {package name}
```

That is removing all app-related data from the device (shared preferences, databases, accounts, etc.)
{% endtab %}

{% tab title="iOS" %}
The command is removing the contents of the application's data folder. An equivalent `idb` command would be:

```
idb file rm --application {bundle id}/
```

[It's also possible to use `xcrun simctl` for that.](https://stackoverflow.com/a/56746729/7009800)
{% endtab %}
{% endtabs %}
