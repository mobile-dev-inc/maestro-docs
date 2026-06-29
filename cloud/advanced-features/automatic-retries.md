---
description: >-
  There are situations where Maestro Cloud will automatically retry a test
  execution
---

# Automatic Retries

### Smart Retries

We automatically retry tests that we consider might be a flaky test - perhaps there was a network hiccup, a timing issue in your test, or something happened on your test environment's backend.

We automatically retry a failed run when we detect that:

1. the previous run of the same flow (as determined by the `name`, or the filename if there isn't one) succeeded (irregardless of branch source
2. it used the exact same target device (os/model)



### Infrastructure-triggered retries

Operating systems are complex, and our device hosts have a virtual device operating system running on top. We're regularly improving device behaviours, but sometimes hiccups occur on a machine or on a network. When this happens and we detect that it was probably infrastructural, we automatically retry your test on a different machine.
