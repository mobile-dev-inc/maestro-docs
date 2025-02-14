# Execution Order

By default, Robin will run the Flows from your upload in parallel, however, that are some cases when a sequential order is needed.

To run your Flows in Robin in a given order you can add the following configuration to your `config.yaml` file:

```yaml
# config.yaml
executionOrder:
    continueOnFailure: false # default is true
    flowsOrder:
        - flowA
        - flowB
```

This configuration describes to our backend the order of the Flows you want to run. The list accepts either the Flow file names (without the `.yaml` extension) or the Flow name (see [Flow Configuration](../../api-reference/configuration/flow-configuration.md)).

The `continueOnFailure` flag determines whether if Robin should proceed with the execution of subsequent Flows if a previous one fails. As an example: if `flowA` fails and `continueOnFailure` is `true`, `flowB` will be executed. If the flag is `false`, `flowB` won't be executed.

Even though the benchmarks will run in serial order, important to say that **we don't reuse the same device.** Each Flow will run on a brand-new device. This means it's not possible to share some internal app states across Flows.

#### Configuring part of the Flows to run sequentially

For instance, if you have three Flows `flowA`, `flowB` and `flowC` and you want to run only `flowA` and `flowB` sequentially. In that case, don't add `flowC` to the list and Robin will run it in parallel with the sequential Flows. This is useful to have a faster turnaround time to get feedback on test cases.
