---
description: A complete example using Maestro + Wikipedia App
---

# Advanced: Wikipedia Android

## Content

* Go through onboarding
* Navigate dashboard
  * Scroll feed & search for item
  * Copy text & paste
  * Validate visible items
* Authentication
  * Signup
  * Login
* Use javascript

{% embed url="https://youtu.be/qmEy_0VRHq8" %}

{% hint style="info" %}
Use `maestro download-samples` to download the app and code
{% endhint %}

## Onboarding

1. Launches app in clear state
2. Runs onboarding flow
   1. Add language
   2. Remove language
   3. Complete onboarding

```yaml
# run-test.yml
appId: org.wikipedia
---
- launchApp:
    clearState: true
- runFlow: "onboarding/main.yml"
```

{% tabs %}
{% tab title="main.yml" %}
```yaml
# onboarding/onboarding.yml
appId: org.wikipedia
---
- runFlow: "add-language.yml"
- runFlow: "remove-language.yml"
- tapOn: "Continue"
- assertVisible: "New ways to explore"
- tapOn: "Continue"
- assertVisible: "Reading lists with sync"
- tapOn: "Continue"
- assertVisible: "Send anonymous data"
- tapOn: "Get started"
```
{% endtab %}

{% tab title="add-language.yml" %}
```yaml
# onboarding/add-language.yml
appId: org.wikipedia
---
- tapOn: "ADD OR EDIT.*"
- tapOn: "ADD LANGUAGE"
- tapOn:
    id: ".*menu_search_language"
- inputText: "Greek"
- assertVisible: "Ελληνικά"
- tapOn: "Ελληνικά"
- tapOn: "Back"
```
{% endtab %}

{% tab title="remove-language.yml" %}
```yaml
# onboarding/remove-language.yml
appId: org.wikipedia
---
- tapOn: "ADD OR EDIT.*"
- tapOn: "More options"
- tapOn: "Remove language"
- tapOn:
    id: ".*wiki_language_checkbox"
    index: 1
- tapOn:
    id: ".*menu_delete_selected"
- tapOn: "OK"
- assertNotVisible: "Ελληνικά"
- tapOn: "Back"
```
{% endtab %}
{% endtabs %}

```sh
maestro test run-test.yml
```

{% embed url="https://youtu.be/AR8ISrzhVeA" %}

### Navigate main dashboard

1. Search & Save
   1. Searches for a wiki page
   2. Saves the wiki page in favorites
   3. Returns to main dashboard
2. Feed
   1. Scroll feed until it finds a particular article
   2. Opens article
3. Copy & Paste
   1. Scrolls feed until it finds a particular article
   2. Copies article title
   3. Pastes copied text into another field
4. Saved
   1. Vaidates a particular page has been saved in our favorites

```yaml
# run-test.yml
appId: org.wikipedia
---
- launchApp
- runFlow: "dashboard/search.yml"
- runFlow: "dashboard/feed.yml"
- runFlow: "dashboard/copy-paste.yml"
- runFlow: "dashboard/saved.yml"
```

{% tabs %}
{% tab title="search.yml" %}
```yaml
appId: org.wikipedia
---
- tapOn: "Search Wikipedia"
- inputText: "Sun"
- assertVisible: "Star in the Solar System"
- tapOn:
    id: ".*page_list_item_title"
- tapOn:
    id: ".*page_save"
- back
- back
```

{% embed url="https://youtu.be/lUVnvTZi1aA" %}
{% endtab %}

{% tab title="feed.yml" %}
```yaml
appId: org.wikipedia
---
- tapOn: "Explore"
- scrollUntilVisible:
    element: "Today on Wikipedia.*"
- tapOn: "Today on Wikipedia.*"
- back
```

{% embed url="https://youtu.be/Sn924uHpsH4" %}
{% endtab %}

{% tab title="copy-paste.yml" %}
```yaml
appId: org.wikipedia
---
- tapOn: "Explore"
- scrollUntilVisible:
    element: "Top read"
- copyTextFrom:
    id: ".*view_list_card_item_title"
    index: 0
- tapOn: "Explore"
- tapOn: "Search Wikipedia"
- inputText: "${maestro.copiedText}"
- back
- back
```

{% embed url="https://youtu.be/iiv7A1TIFcU" %}
{% endtab %}

{% tab title="saved.yml" %}
```yaml
appId: org.wikipedia
---
- tapOn: "Saved"
- tapOn: "Default list for your saved articles"
- assertVisible: "Sun"
- assertVisible: "Star in the Solar System"
- back
```

{% embed url="https://youtu.be/V_mVRicKEnU" %}
{% endtab %}
{% endtabs %}

```sh
maestro test run-test.yml
```

### Authentication

1. Signup
   1. Navigates to signup
   2. Generates credentials using javascript
   3. Fills input fields with generated credentials
2. Login
   1. Navigates to login
   2. Fetches a test user from a test api using javascript
   3. Fill input fields with fetched credentials

```yaml
# run-test.yml
appId: org.wikipedia
---
- launchApp
- runFlow: "auth/signup.yml"
- runFlow: "auth/login.yml"
```

{% tabs %}
{% tab title="login.yml" %}
```yaml
appId: org.wikipedia
---
- tapOn: "More"
- tapOn: "LOG IN.*"
- tapOn:
    id: ".*create_account_login_button"
- runScript: "fetchTestUser.js"
- tapOn: "Username"
- inputText: "${output.test_user.username}"
- tapOn: "Password"
- inputText: "test-password"
- tapOn: "LOG IN"
# we won't actually login

- back
- back
```

{% embed url="https://youtu.be/AUxW_shTg7I" %}
{% endtab %}

{% tab title="signup.yml" %}
```yaml
appId: org.wikipedia
---
- tapOn: "More"
- tapOn: "LOG IN.*"
- runScript: "generateCredentials.js"
- tapOn: "Username"
- inputText: "${output.credentials.username}"
- tapOn: "Password"
- inputText: "${output.credentials.password}"
- tapOn: "Repeat password"
- inputText: "${output.credentials.password}"
- tapOn: "Email.*"
- inputText: "${output.credentials.email}"
# We won't actually create the account

- back
- back
```

{% embed url="https://youtu.be/bqG-n9sAUVI" %}
{% endtab %}
{% endtabs %}

#### Javascript scripts

{% tabs %}
{% tab title="generateCredentials.js" %}
```javascript
function username() {
  const date = new Date().getTime().toString();
  return `test_user_${date}`;
}

function email() {
  const date = new Date().getTime().toString();
  return `test-user-${date}@test.com`;
}

function password() {
  const date = new Date().getTime().toString();
  return `test-user-password-${date}`;
}

output.credentials = {
  email: email(),
  password: password(),
  username: username(),
};

```
{% endtab %}

{% tab title="fetchTestUser.js" %}
```javascript
// Fetches test user from API
function getTestUserFromApi() {
  const url = `https://jsonplaceholder.typicode.com/users/1`;
  const response = http.get(url);
  const data = json(response.body);

  return {
    username: data.username,
    email: data.email,
  };
}

output.test_user = getTestUserFromApi();
```
{% endtab %}
{% endtabs %}

```bash
maestro test run-test.yml
```
