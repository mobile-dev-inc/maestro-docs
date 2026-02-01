# FAQ

Find answers to common Maestro questions: parameters, assertions, YAML gotchas, cloud behavior, and how to organize your tests.

<details>

<summary>How can I use the same flow when my apps have different app IDs?</summary>

Use an [external parameter](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/flow-control-and-logic/parameters-and-constants) for `appId` and pass it when you run Maestro. For example, pass `APP_ID` when testing with the Maestro CLI:

```bash
maestro test -e APP_ID=your.app.id file.yaml
```

In your Flow, refer to it with `${APP_ID}`:

```yaml
appId: ${APP_ID}
---
- launchApp
```

</details>

<details>

<summary>How do I assert on a string that contains a dollar sign?</summary>

Maestro treats `$` as the start of a variable. Escape the dollar so it is treated as literal text:

```yaml
- assertVisible: \$150 in Cash
```

</details>

<details>

<summary>How do I compare two values?</summary>

To assert on values that appear on different screens, store each value in a variable with [`copyTextFrom`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/copytextfrom) and [`evalScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/evalscript), then compare in a `runFlow` with a `when` condition:

```yaml
# Navigate to first value, then:
- copyTextFrom:
    id: 'listView1'
- evalScript: ${output.firstPrice = maestro.copiedText}

# Navigate to second value, then:
- copyTextFrom:
    id: 'detailView'
- evalScript: ${output.secondPrice = maestro.copiedText}

# Compare:
- runFlow:
    when:
      true: ${output.firstPrice === output.secondPrice}
    commands:
      - evalScript: ${console.log('Prices match! Both are ' + output.secondPrice)}
```

</details>

<details>

<summary>How do I generate a random number?</summary>

Maestro provides commands for generating random strings and names, but it does not include a built-in command for generating random numbers. To generate a random number, you can use JavaScript via [`runScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/runscript).

The following example shows how to create a script (`randomNumber.js`) that generates an 8-digit random number:

```javascript
// Generate an 8-digit random number
output.randomNumber = Math.floor(Math.random() * 90000000) + 10000000;
```

To use this value in your flow, run the script to populate the [`output`](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/javascript/manage-data-and-states) object, then reference it in a JavaScript expression using [`evalScript`](https://app.gitbook.com/s/HqSeOOzxPCLfnK9YzOkb/commands-available/evalscript):

```yaml
- runScript: ../scripts/randomNumber.js
- evalScript: ${EMAIL = "maestro+" + output.randomNumber + "@domain.com"}
```

This assigns the generated value to the Maestro variable `EMAIL`, which can be reused later in the flow.

</details>

<details>

<summary>Why does YES get translated to true, and NO to false?</summary>

If you use `tapOn: YES` or `tapOn: NO`, Maestro may interpret them as booleans and attempt to find the text `"true"` or `"false"` instead:

```yaml
appId: com.example
---
- launchApp
- tapOn: YES
```

You may see an error like:

```bash
 ║  > Flow: flow                         
 ║                                       
 ║    ❌   Tap on "true"                 
 ║                                       
                                         
Element not found: Text matching regex: true

Element with Text matching regex: true not found. Check the UI hierarchy in debug artifacts to verify if the element exists.
```

This behavior comes from YAML itself. The [YAML specification](https://yaml.org/type/bool.html) allows booleans to be written as `true`/`false`, `yes`/`no`, `on`/`off`, or `Y`/`N` (in various casings). As a result, unquoted `YES` and `NO` are parsed as booleans.

To work around this, force the value to be treated as literal text by quoting it, or use a regular expression:

```yaml
- tapOn: "YES"
- tapOn: ^No    # Text that begins with "No"
```

</details>

<details>

<summary>Why are my tests slower in Maestro's cloud environment?</summary>

The cloud environment prioritizes reliability and repeatability: each device is wiped and recreated between tests so one run cannot affect another. That adds about 2–4 minutes between tests compared with running locally.

To reduce total run time:

* Add more parallel runners.
* Restructure tests into fewer, longer flows, without sacrificing reliability or useful failure information.

</details>

