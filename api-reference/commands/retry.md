# retry

Some flaky behaviour is expected or beyond an app's control. For those situations, it can be useful having a small controlled loop that will retry one or more commands a limited number of times.

```yaml
- retry:
    maxRetries: 3
    commands:
      - tapOn:
          id: 'button-that-might-not-be-here-yet'
```

## Parameters

`maxRetries` is an integer indicating the number of times to attempt the flow. Minimum 0, maximum 3. Defaults to 1 retry attempt.

`commands` is a list of commands to run. This, or `file`, must be provided.

`file` is a reference to another flow to attempt. This, or `commands`, must be be provided (but not both).

Like other commands, this accepts the default parameters, such as `label`, `optional` and `env`.
