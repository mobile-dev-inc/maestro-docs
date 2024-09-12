# Commands

The Flow steps you define in YAML are called **commands**.

## Labels

Each Maestro command accepts an optional `label` attribute that lets you
customize the command's name:

```yaml
- tapOn:
    id: buy-now
    label: Tap on Buy Now button
    
- inputText:
    label: Input the company email
    text: maestro@mobile.dev

- swipe:
    direction: LEFT
    label: Swipe for onboarding
```

```
✅ Tap on Buy Now button
✅ Input the company email
✅ Swipe for onboarding
```

Setting a label can have an additional advantage of being able to remove
sensitive content from console output, for example this:

```
✅ Tap on "Password"
✅ Input text "mySecr3tPassw0rd!"
```

becomes:

```
✅ Tap on "Password"
✅ Enter the test user's password
```

{% hint style="warning" %}
The values will still appear in the logs of the run.
{% endhint %}

Labels are also a useful alternative to comments for contributors trying to
understand the intent of a particular step.

```yaml
- extendedWaitUntil:
    visible: Recommended Products
    timeout: 5000
    label: Wait for all personalized content to load
```

## Optional

Each Maestro command accepts an optional `optional` attribute that lets control
what should happen if the command fails.

```yaml
- launchApp: com.example.example
- assertVisible:
    text: Summer sale is here!
    optional: true
- tapOn: Sign up now!
```

If `optional` is set to `true`, the flow will continue executing even if the
command fails. The warning will be displayed:

```
✅ Launch app "com.example.example"
⚠️  Assert that "Summer sale is here!" is visible (warned)
✅ Tap on "Sign up now!"
```

The default value of `optional` for almost all commands is `false`, which means
that the flow will stop executing if any command fails. The only exception (at
least for now) are AI-powered commands, which have `optional` set to `true` by
default.

## All commands
