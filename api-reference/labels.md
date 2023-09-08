# Labels

We believe that easy-to-read tests are important. That's why we've added the ability to add labels to your tests. Labels are a way to add metadata to any test command. For example, you can add a label to a `tapOn` command to make it easier to understand what view you're tapping on, where the text or id isn't obvious.

```yaml
- tapOn:
    id: "close"
    label: "Close content popup overlay"
```

This can be especially useful for other contributors (or your future self!) trying to understand what the test is doing, or why a particular step exists.

```yaml
- extendedWaitUntil:
    visible: "New in"
    timeout: 5000
    label: "Wait for all personalised content to load before continuing"
```

Labels used for any command will also be used for the terminal output, making it easier to understand (and debug) what's going on. This has an added advantage of being able to obscure text from console output that you want to keep out of your logs.

```
✅ Tap on "Password"
✅ Input text "mySecr3tPassw0rd!"
```
becomes
```
✅ Tap on "Password"
✅ Enter the test user's password
```
