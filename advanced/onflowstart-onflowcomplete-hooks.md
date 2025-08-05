---
description: >-
  Configure hooks onFlowStart and onFlowComplete to run scripts or flows before
  and after the main flow.
---

# onFlowStart / onFlowComplete hooks

### General

If some logic needs to be executed before the start or after the completion of maestro flow onStart and onComplete hooks can be used.\
\
The hooks are a part of [flow configuration section](../api-reference/configuration/flow-configuration.md).

Basic usage of an API could look like that:

```
# flow.yaml
appId: my.app
onFlowStart:
  - runFlow: setup.yaml
  - runScript: setup.js
  - <any other command>
onFlowComplete:
  - runFlow: teardown.yaml
  - runScript: teardown.js
  - <any other command>
```

### What if one of the hooks fails?

In case of either **onFlowStart** / **onFlowComplete** failure the behavior of maestro is consistent with JUnit (@before / @after) and XCTest (setup / teardown) hooks.

| Test case                                                                        | Behavior                            |
| -------------------------------------------------------------------------------- | ----------------------------------- |
| when before onFlowStart hook fails, does that fail the whole flow?               | flow marked 🔴                      |
| when onFlowStart hook fails, does that skip the main body of the flow execution? | flow execution skipped              |
| when onFlowStart hook fails, does the onFlowComplete hook still run?             | onFlowComplete hook is still called |
| when the onFlowComplete hook fails, does the flow fail?                          | flow marked 🔴                      |

### onFlowStart / onFlowComplete in the subflows

If either **`onFlowStart`** or **`onFlowComplete`** hooks are implemented within a [subflow](../api-reference/commands/runflow.md), their commands will execute as expected. However, note that the execution start and end times will correspond to the subflow's duration, not the main flow's.
