# FAQ

Find answers to common Maestro questions: parameters, assertions, YAML gotchas, cloud behavior, and how to organize your tests. If you don't find your issue here, check Known issues or Bug report.

<details>

<summary>How can I use the same flow when my apps have different app IDs?</summary>

Use an external parameter for `appId` and pass it when you run Maestro. For example, pass `APP_ID`:

```bash
maestro test -e APP_ID=your.app.id file.yaml
```

In your flow, refer to it with `${APP_ID}`:

```yaml
appId: ${APP_ID}
---
- launchApp
```

For more on parameters, see Parameters and constants.

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

To assert on values that appear on different screens, store each value in a variable with `copyTextFrom` and `evalScript`, then compare in a `runFlow` with a `when` condition:

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

Maestro has commands for random strings and names but not for random numbers. Use JavaScript (for example with `runScript`) to generate a number in the range you need.

**Script (e.g. `randomNumber.js`):**

```javascript
// Generate an 8-digit random number
output.randomNumber = Math.floor(Math.random() * 90000000) + 10000000;
```

**Flow:**

```yaml
- runScript: ../scripts/randomNumber.js
- evalScript: ${EMAIL = "maestro+" + output.randomNumber + "@domain.com"}
```

</details>

<details>

<summary>Why does YES get translated to true, and NO to false?</summary>

If you use `tapOn: YES` or `tapOn: NO`, Maestro may treat them as booleans and look for the text `"true"` or `"false"`:

```yaml
appId: com.example
---
- launchApp
- tapOn: YES
```

You can get an error like:

```plaintext
Element not found: Text matching regex: true
```

This comes from YAML: the [YAML specification](https://yaml.org/type/bool.html) allows booleans to be written as `true`/`false`, `yes`/`no`, `on`/`off`, or `Y`/`N` (and various casings). So unquoted `YES` and `NO` are parsed as booleans.

**Fix:** Force the literal text by quoting, or use a regex:

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
* Restructure tests into fewer, longer flows—without sacrificing reliability or useful failure information.

</details>

<details>

<summary>How do I organize my repository for Maestro tests?</summary>

Many teams keep Maestro tests next to their app code so that a given build has the right tests and branches can evolve flows and features together. Two common ways to lay out flows:

**Journeys** — Group flows by user journey (e.g. new vs existing users). Start with a single `flows` folder and add subfolders when needed:

```
├── flows
│   ├── config.yaml
│   ├── login.yaml
│   ├── register.yaml
│   └── shopping.yaml
└── src
    └── app
        └── <app code>
```

As the suite grows, you can split by journey and add shared utils:

```
├── flows
│   ├── config.yaml
│   ├── tests
│   │   ├── new_users
│   │   │   ├── register.yaml
│   │   │   └── shopping_first_time_discount.yaml
│   │   └── existing_users
│   │       ├── login.yaml
│   │       ├── shopping.yaml
│   │       └── ...
│   └── utils
│       └── set_discount_code.js
└── src
    └── app
        └── <app code>
```

You can set inclusion patterns in `config.yaml` so only the tests you want are run (see Test discovery and tags).

**Features** — Mirror your app’s feature structure so flows are easy to find and maintain:

```
├── flows
│   ├── config.yaml
│   ├── account
│   │   └── set_display_name.yaml
│   ├── auth
│   │   ├── login.yaml
│   │   ├── login_invalid.yaml
│   │   └── login_locked_account.yaml
│   ├── basket
│   │   ├── add_to_cart.yaml
│   │   └── update_cart.yaml
│   └── checkout
│       ├── complete_purchase.yaml
│       └── save_for_later.yaml
└── src
    └── app
        ├── account
        ├── auth
        ├── basket
        └── checkout
```

Choose the structure that fits how you think about and run your tests.

</details>

### Related content

* Known issues: Known limitations and workarounds.
* Bug report: How to report a new issue.
