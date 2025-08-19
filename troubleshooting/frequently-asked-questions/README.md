# Frequently Asked Questions

### How can I use the same flow when my apps have different app IDs?

If you want to run the same flow for apps with different app IDs, you can use an [external parameter](../../advanced/parameters-and-constants.md) for `appId`. Pass the parameter `APP_ID` to Maestro:

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



### How do I generate a random number?

Whilst there are commands for random strings and names, there's no function for generating random numbers. Users can use JavaScript to generate a number in the range they need.

randomNumber.js :

```javascript
// Generate an 8 digit random number
output.randomNumber = Math.floor(Math.random() * 90000000) + 10000000;
```

flow.yaml:

```yaml
- runScript: ../scripts/randomNumber.js
- evalScript: ${EMAIL = "maestro+" + output.randomNumber + "@domain.com"}
```



### Why are my tests slower in Maestro's cloud environment?

The cloud environment optimises for reliability and repeatability, on the belief that slower correct results beat faster inconsistent results, every time. Each device, between one test and the next, is wiped and recreated, so that there's no chance of any test ever affecting any other. Compared with running locally, this adds 2-4 minutes between tests. To improve total time to finish a run, consider adding additional parallel runners. Another option is restructuring your tests for fewer longer tests, but be sure you're not making the same mistake, and sacrificing reliability or information in favour of speed.
