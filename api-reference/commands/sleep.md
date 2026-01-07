# sleep

`sleep` pauses the flow execution for a specified duration.

```yaml
- sleep: 100     # Sleeps for 100ms (default unit is ms)
- sleep: 1000ms  # Sleeps for 1000ms
- sleep: 1s      # Sleeps for 1 second
- sleep:
    time: 2000
    label: Pause for two seconds
```

Note: This command shouldn't be necessary in most situations. Use [assertVisible](./assertvisible.md) or [extendedWaitUntil](./extendedwaituntil.md) to wait for something to appear. This command should be used in situations where an external system is performing a task that you cannot see the effect of (e.g. server-side transaction processing), or a splash animation that cannot be represented in the Maestro hierarchy that needs to be awaited.
