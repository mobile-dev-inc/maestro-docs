# Frequently Asked Questions

### How can I use the same flow when my apps have different app IDs?

If you want to run the same flow for apps with different app IDs, you can use an [external parameter](../advanced/parameters-and-constants.md) for `appId`. Pass the parameter `APP_ID` to Maestro:

```
maestro test -e APP_ID=your.app.id file.yaml
```

And then refer to it in your flow using `${APP_ID}`:

```yaml
appId: ${APP_ID}
---
- launchApp
```

### How do I assert on a string that contains a dollar sign?

Values with dollar signs can be interpreted as variables. To avoid this, escape the dollar characters.

```yaml
- assertVisible: \$150 in Cash
```

### How do I compare two values?

To assert on values that exist on different screens, store them in variables.

```yaml
# Perform steps to navigate to first value, then:
- copyTextFrom: 
    id: 'listView1'
- evalScript: ${output.firstPrice = maestro.copiedText}

# Perform steps to navigate to the second value, then:
- copyTextFrom: 
    id: 'detailView'
- evalScript: ${output.secondPrice = maestro.copiedText}

# Compare the values:
- runFlow:
    when:
      true: ${output.firstPrice === output.secondPrice}
    commands:
      - evalScript: ${console.log('Prices match! Both are ' + output.secondPrice)}
```
