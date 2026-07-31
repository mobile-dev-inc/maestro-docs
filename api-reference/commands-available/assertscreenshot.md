---
description: >-
  Perform visual regression testing of your application against existing
  screenshots
---

# assertScreenshot

The `assertScreenshot` command takes a screenshot and matches it against a known good image, performing a visual regression test.

The assertion will fail if the comparison image is too dissimilar, or doesn't exist.

### Syntax

```yaml
- assertScreenshot: splash.png
```

or

```yaml
- assertScreenshot:
    path: screen.png
    cropOn:
      id: banner
    thresholdPercentage: 98
```

### Parameters

| Parameter             | Type             | Description                                                                                                                                                                                                                                                  |
| --------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `path`                | String           | Path to the reference screenshot that the current screen will be compared against. Can be a JavaScript expression. Was likely created by a [takeScreenshot](takescreenshot.md) invocation in a previous run.                                                 |
| `cropOn`              | Element Selector | Optional. A selector to narrow the screenshot before comparison. The comparison screenshot must also have been cropped. For a complete list of all available selectors, see the [Selectors](https://docs.maestro.dev/api-reference/selectors) documentation. |
| `thresholdPercentage` | Number           | Optional. Percentage match required to pass this assertion. Default is `95`. Can be a variable or a JavaScript expression, as long as it resolves to a number.                                                                                               |
| `label`               | String           | Optional. A message to display when executing the evaluation.                                                                                                                                                                                                |

### Usage Examples

#### Assert against a reference screenshot

This example compares the current screen against `splash.png`, using the default threshold of 95%.

```yaml
- assertScreenshot: splash.png
```

#### Set the threshold from a variable

The threshold is interpolated before the comparison runs, so you can tune it per environment or per device without editing the Flow.

```yaml
appId: com.example.app
env:
  THRESHOLD_PERCENTAGE: 80
---
- assertScreenshot:
    path: ./screenshot.png
    thresholdPercentage: ${THRESHOLD_PERCENTAGE}
```

{% hint style="info" %}
The value must resolve to a number. If it resolves to something else — an empty string from an unset variable, for example — the assertion fails with `Invalid thresholdPercentage for assertScreenshot` rather than falling back to the default.
{% endhint %}
