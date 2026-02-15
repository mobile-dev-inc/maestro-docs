---
description: Retry a block of commands on failure with configurable attempts.
---

# retry

The `retry` command executes a set of commands repeatedly until they succeed or the maximum number of retries is reached. Use this command to handle intermittent or unpredictable behavior in your application.

### Parameters

The `retry` command accepts the following parameters:

| Parameter    | Description                                                                                                                |
| ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `maxRetries` | **Optional.** Specifies the number of times to retry the commands. The value must be between `0` and `3`. Defaults to `1`. |
| `commands`   | A list of commands to execute. You must provide either `commands` or `file`.                                               |
| `file`       | The path to a file containing a flow to execute. You must provide either `file` or `commands`.                             |

### Usage examples

The following example retries tapping a button up to three times. If the process is successful on the second attempt, the test will proceed to the next step, considering this one successful.

```yaml
- retry:
    maxRetries: 3
    commands:
      - tapOn:
          id: 'button-that-might-not-be-here-yet'
```
