# Make HTTP requests

Maestro includes a built-in JavaScript HTTP client that allows you to interact with external APIs directly from your test flows. This is particularly useful for setting up test data, authenticating users, or verifying backend state without navigating through the UI.

### Making Requests

The Maestro HTTP client is a wrapper around okhttp3 and provides simple methods for common HTTP verbs.

You can use the following shorthand methods for standard requests:

* `http.get(url, config)`
* `http.post(url, config)`
* `http.put(url, config)`
* `http.delete(url, config)`

For other methods (like `PATCH` or `OPTION`), use the generic `request` function:

```javascript
const response = http.request('https://example.com', {
    method: "PATCH",
    body: JSON.stringify({ status: "active" })
});
```

### Working with JSON

Maestro provides a global `json()` function to parse HTTP response bodies into JavaScript objects.

For example, assume that `https://api.example.com/user/1` returns the following JSON response:

```json
{
  "id": 1,
  "email": "user@example.com",
  "profile": {
    "name": "Jane Doe",
    "age": 32
  }
}
```

You can parse the response body and access fields directly:

```js
// script.js
const response = http.get('https://api.example.com/user/1');

// Parse the body and access fields directly
const userData = json(response.body);
output.username = userData.profile.name;
```

In this example, the user’s name is read from `profile.name` and assigned to `output.username`.

### Configuration Options

When making a request, you can pass a configuration object to define headers, bodies, or form data.

#### Headers

Pass custom headers, such as authentication tokens or content types, using the `headers` property.

```javascript
const response = http.get('https://example.com', {
    headers: {
        'Authorization': 'Bearer ' + output.token,
        'Content-Type': 'application/json'
    }
});
```

#### Request Body

For `POST`, `PUT`, or `PATCH` requests, provide the payload in the `body` parameter. Remember to stringify JSON objects.

```javascript
const response = http.post('https://example.com/login', {
    body: JSON.stringify({
        username: "test_user",
        password: "password123"
    })
});
```

#### Multipart Form Data

To upload files or send multipart data, use the `multipartForm` parameter. When sending files, the following parameters are available:

* `filePath`: The path to the file. It is **required** for file uploads.
* `mediaType`: The MIME type of the file (optional).

```javascript
// script.js
const response = http.post('https://example.com/myEndpoint', {
    multipartForm: {
      "uploadType": "import",
      "data": {
        "filePath": filePath,
        "mediaType": "text/csv"
      }
    },
})
```

{% hint style="info" %}
If both `body` and `multipartForm` are provided in one request, the `body` parameter will be ignored.
{% endhint %}

### The `response` object

Every HTTP call returns a `response` object containing the following fields:

<table data-header-hidden><thead><tr><th width="114.22222900390625"></th><th width="93.111083984375"></th><th></th></tr></thead><tbody><tr><td><strong>Field Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td><code>ok</code></td><td>Boolean</td><td><code>true</code> if the request was successful (status 200-299).</td></tr><tr><td><code>status</code></td><td>Number</td><td>The HTTP status code (e.g., <code>200</code>, <code>404</code>).</td></tr><tr><td><code>body</code></td><td>String</td><td>The raw string body of the response.</td></tr><tr><td><code>headers</code></td><td>Object</td><td>HTTP response headers (multiple values are comma-separated).</td></tr></tbody></table>

### Example: Authenticated API Setup

A common pattern is to authenticate via API and store the token in the `output` object for subsequent UI steps.

```javascript
// setup.js
const loginResponse = http.post('https://my-api.com/login', {
    body: JSON.stringify({ user: "admin", pass: "secret" }),
    headers: { 'Content-Type': 'application/json' }
});

const data = json(loginResponse.body);

// Store the token globally for use in the Flow
output.api = {
    token: data.token,
    userId: data.userId
};
```



```yaml
# flow.yaml
appId: com.example.app
---
- runScript: setup.js
- evalScript: ${console.log('Logged in user: ' + output.api.userId)}
- tapOn: "Profile"
## Use the captured token in a later UI-based network call if needed
```

