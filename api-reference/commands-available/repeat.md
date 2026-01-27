# repeat

The `repeat` command executes a sequence of commands multiple times, either for a fixed number of iterations or until a specific condition is met.

### Parameters

To customize sequence execution when using the `repeat` command, you can use the following parameters:

<table><thead><tr><th width="122">Parameter</th><th width="122">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>times</code></td><td><code>integer</code></td><td>The number of times to repeat the <code>commands</code>.</td></tr><tr><td><code>while</code></td><td><code>condition</code></td><td>A condition that must evaluate to <code>true</code> for the loop to continue. The loop terminates when the condition becomes <code>false</code>.</td></tr><tr><td><code>commands</code></td><td><code>list</code></td><td>The list of commands to execute during each iteration.</td></tr></tbody></table>

### Usage examples

#### Repeat a specific number of times

To execute a set of commands a fixed number of times, use the `times` parameter.

```yaml
- repeat:
    times: 3
    commands:
      - tapOn: Button
      - scroll
```

In the above example, the test will repeat the process of tapping on the button and scrolling three consecutive times.

#### Repeat while a condition is true

To execute commands as long as a condition is met, use the `while` parameter. The loop continues as long as the element with the text `ValueX` is not visible.

```yaml
- repeat:
    while:
      notVisible: "ValueX"
    commands:
      - tapOn: Button
```

#### Repeat using a JavaScript expression

The `while` parameter also accepts a JavaScript expression. The loop continues as long as the expression evaluates to `true`.

```yaml
- evalScript: ${output.counter = 0}
- repeat:
    while:
      true: ${output.counter < 3}
    commands:
      - tapOn: Button
      - evalScript: ${output.counter = output.counter + 1}
```

#### Repeat with a maximum count and a condition

You can combine `times` and `while` to repeat commands until a condition is met, but for no more than a specified number of iterations. The loop stops when either the `while` condition becomes `false` or the `times` count is reached, whichever occurs first.

The following example taps a button while an element is not visible, but stops after 10 attempts regardless of the element's visibility.

```yaml
- repeat:
    times: 10
    while:
      notVisible: "someElement"
    commands:
      - tapOn: Button
```

Here’s another example that logs `"Hello World"` four times. The `times: 4` limit ensures the loop stops even if the condition never becomes false. For example, if the counter were never incremented.

```yaml
- evalScript: ${output.counter = 1}
- repeat:
    times: 4
    while:
      true: ${output.counter < 10}
    commands:
      - evalScript: ${console.log("Hello World")}
      - evalScript: ${output.counter++}
```

{% hint style="success" %}
Use the `--verbose` flag to see the effect of the `repeat` command more effectively when using [Maestro CLI overview](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/ "mention").
{% endhint %}

### Related content

Learn how to use [conditions](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/conditions) in your Flows.
