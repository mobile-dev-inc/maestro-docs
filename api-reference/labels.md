# Labels

For each Maestro command, you can add a label attribute that will help you to customize the CLI output:

```yaml
- tapOn:
    id: "buy-now"
    label: "Tap on Buy Now button"
    
- inputText:
    label: "Input the mobile.dev email"
    text: maestro@mobile.dev

- swipe:
    direction: LEFT
    label: "Swipe for onboarding"
```

This has an added advantage of being able to remove sensitive content from console output. _Note: values will still appear in the logs of the run_

```
✅ Tap on "Password"
✅ Input text "mySecr3tPassw0rd!"
```

becomes

```
✅ Tap on "Password"
✅ Enter the test user's password
```

Labels are also a useful alternative to comments for contributors trying to understand the intent of a particular step.

```yaml
- extendedWaitUntil:
    visible: "Recommended Products"
    timeout: 5000
    label: "Wait for all personalised content to load"
```
