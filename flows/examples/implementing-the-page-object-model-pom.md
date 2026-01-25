# Implementing the Page Object Model (POM)

As the number of test grows, one problem shows up quickly, you will use selectors in every Flow file.

Hardcoded `id` spread across dozens of YAML files are easy at first, but the moment a developer renames a button or changes a label, you may find yourself updating several tests just to fix one UI change. This is an example of a not escalable approach.

This is exactly the problem the **Page Object Model (POM)** is designed to solve.

POM is a design pattern that introduces an abstraction layer between your test logic and your UI selectors. Instead of referencing element `id` directly in your Flows, you reference a central JavaScript object. When the UI changes, you update the selector in one place, and every test that depends on it keeps working.

In summary, your tests become easier to read, easier to maintain, and far more resilient.

### The core idea

The guiding principle behind POM is simple:

> Separate **what an element is** from **how your test interacts with it**.

You achieve this by:

1. Defining selectors in JavaScript files using the `output` object.
2. Loading those definitions at runtime.
3. Referencing variables (not raw `id`) in your Flows.

Once you adopt this pattern, your Flows describe user intent, not technical implementation details.

### The basic workflow

At a high level, implementing POM follows this workflow:

1. Store `id`, `text`, or regex patterns in `.js` files using `output`.
2. Group selectors logically by screen, feature, or platform.
3. Use `runScript` directly or a centralized loader Flow to make selectors available.
4. Reference selectors using `${output...}` in `tapOn`, `inputText`, `assertVisible`, and other commands.

The following sections describe how you can adopt the POM approach.

#### 1. Define your first page object

Start by creating a JavaScript file that represents a screen in your app. For example, a login screen.

```javascript
// login.js
output.login = {
    email: 'email_text',
    password: 'password_text',
    loginBtn: 'loginButton',
    registerBtn: 'registerButton'
}
```

This file acts like a dictionary for the Login screen. Each key describes what the element is, while the value defines how Maestro can find it.

To use the the element selectos, you need to use `runScript` to load the screen element variables. As a result, there are no raw IDs scattered throughout the test, and the intent of each action is immediately clear.

```yaml
# login_flow.yaml
---
- runScript: login.js

- tapOn:
    id: ${output.login.email} 
- inputText: "simon@maestro.com"

- tapOn: 
    id: ${output.login.password} 
- inputText: ${PASSWORD}

- tapOn: 
    id: ${output.login.loginBtn} 
```

#### 2. Organize complex screens with nested objects

As screens grow more complex, a flat list of selectors can become difficult to manage. Using POM, you can nest objects, mirroring the structure of your UI.

This is especially useful for reusable components like cards, toolbars, or navigation menus. The following example shows a object used to describe a card:

```javascript
// cards.js
output.cards = {
    cardTitle: 'card_title',

    virtualCards: {
        createBtn: 'btn_create_virtual',
        details: {
            number: 'card_number',
            expiry: 'card_expiry'
        }
    }
}
```

The structure reflects the UI hierarchy. Related elements live together, and naming collisions are avoided.

The process of using nested selectors in a Flow is similar to working with a JavaScript object defined in a JSON file. The selector path itself documents the UI structure, making tests easier to understand and maintain.

```yaml
- runScript: cards.js

- tapOn: 
    id: ${output.cards.virtualCards.createBtn} 
- assertVisible: 
    id: ${output.cards.virtualCards.details.number} 
```

### POM benefits&#x20;

Using POM is not just a stylistic choice, it fundamentally improves test quality:

* **Centralized maintenance**: If `btn_create_virtual` changes to `fab_add`, you update one file, not dozens of tests.
* **Namespacing**: Nested objects prevent collisions between common names like `title`, `submit`, or `button`.
*   **Regex support**: Maestro treats selector strings as regular expressions by default. You can store dynamic patterns like:

    ```javascript
    output.welcomeBanner = 'Welcome back, .*'
    ```

    and reuse them consistently across tests.
* **Readable failures**: When a test fails, variable names such as `loginBtn` are far more informative than raw IDs.

### Recommended folder structure

Keeping selectors separate from test logic will improve your organization. A dedicated `elements` folder makes this separation explicit.

For cross-platform apps, organizing by platform is also strongly recommended. Your tests remain platform-agnostic, while selectors stay platform-specific.

```
android/
  elements/
    login.js
    home.js
    loadElements.yaml
  tests/
    login_flow.yaml

ios/
  elements/
    login.js
    home.js
    loadElements.yaml
  tests/
    login_flow.yaml
```

### The loader strategy

As your project grows, manually calling `runScript` in every Flow becomes repetitive and error-prone. To solve this problem, you can use a Loader Flow. The loader’s only responsibility is to load all page bjects once, as in the following example:

```yaml
# elements/loadElements.yaml
appId: com.example.app
---
- runScript: cards.js
- runScript: login.js
- runScript: home.js
- runScript: nav.js
```

If you use the loader as a subflow, It initializes your entire selector schema at the beginning of a test run. This way, every test starts from a known, consistent state, and no selector is accidentally forgotten.

```yaml
---
- runFlow: elements/loadElements.yaml
- launchApp
# All selectors are now available via ${output...}
```

### Handle cross-platform differences

Android, iOS, and Web often use different IDs for the same functional element. POM makes this manageable by keeping variable names consistent while swapping implementations.

```yaml
- runFlow:
    when: 
        platform: Android 
    commands:
      - runScript: android/elements/login.js

- runFlow:
    when: 
        platform: iOS
    commands:
      - runScript: ios/elements/login.js
      
- runFlow:
    when: 
        platform: Web
    commands:
      - runScript: web/elements/login.js
```

By applying this approach, each platform loads its own selectors, but your test logic never changes.

```yaml
- tapOn:
  id: ${output.login.loginBtn} 
```

### Related content

To master the logic used in the Page Object Model, explore these deep-dives:

* [Broken link](/broken/pages/8DNy5pvaH9KZZRAImdkh "mention"): Learn how to use JavaScript to manage shared data and complex structures.
* [parameters-and-constants.md](../flow-control-and-logic/parameters-and-constants.md "mention"): Learn how the `output` object persists across Flows.
* [conditions.md](../flow-control-and-logic/conditions.md "mention"): Master the `when` clause for platform-specific logic.
