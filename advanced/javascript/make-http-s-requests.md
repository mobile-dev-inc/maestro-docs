# Make HTTP(s) requests

Maestro comes with its own JavaScript HTTP API

```javascript
// script.js
const response = http.get('https://example.com')

output.script.result = response.body
```

### JSON

Use `json()` function to parse JSON responses.

For example, assume that `https://example.com/jsonEndpoint` returns the following result:

```json
{
    "myField": {
        "mySubField": "Test value"
    }
}
```

`mySubField` could then be accessed in the following way:

```javascript
// script.js
const response = http.get('https://example.com/jsonEndpoint')

output.script.result = json(response.body).myField.mySubField
```

### POST request

To send body to a given endpoint, specify a `body` parameter:

```javascript
// script.js
const response = http.post('https://example.com/myEndpoint', {
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(
        {
            myField: "Payload"
        }
    )
})
```

Setting a `'Content-Type'` header might be required. See [Headers](make-http-s-requests.md#headers).

You can also send multipart form data by specyfying `multipartForm` parameter:
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

In `multipartForm` you can include many fields. It is also possible to upload multiple files in one request by using objects with filePath property.
`filePath` is required for the files. `mediaType` is optional.

> **ℹ️ Note** If you include both `body` and `multipartForm` in one request then `body` will be ignored.

### Headers

Headers can be provided in a `headers` parameter

```javascript
// script.js
const response = http.get('https://example.com', {
    headers: {
        Authorization: 'Bearer MyToken'
    }
})
```

### Other request types

The following request methods are provided out of the box:

* `http.get`
* `http.post`
* `http.put`
* `http.delete`

To send a request of any other HTTP method, use `http.request`

```javascript
// script.js
const response = http.request('https://example.com`, {
    method: "GET"   // or specify any other method, i.e. OPTION
})
```

### Response object

| Field Name | Value                                                                                                               |
| ---------- | ------------------------------------------------------------------------------------------------------------------- |
| `ok`       | `true` if request was successful, `false` otherwise                                                                 |
| `status`   | HTTP status code (i.e. `200`)                                                                                       |
| `body`     | String body of the response                                                                                         |
| `headers`  | response HTTP headers, where each header value is a string (or a comma-separated string in case of multiple values) |

### Example

Here's an example of using these utilities to perform a common test action, creating a user and populating it with data.

```javascript
const date = new Date();
const email = `test${date.getTime().toString()}@test.com`;
const password = 'test'

function createNewUser() {
  const url = 'https://my-api/signup'

  const signupResponse = http.post(url, {
    body: JSON.stringify({
      email: email,
      password: 'test'
    }),
    headers: {'Content-Type': 'application/json'}
  });

  const data = json(signupResponse.body);

  return {
    guid: data.guid,
    token: data.token
  }
}

function fillUserInfo() {
  const test_user = createNewUser()
  const url = `https://my-api/user/${test_user.guid}`

  http.request(url, {
    method: 'PATCH',
    body: JSON.stringify({
      age: '46',
      gender: 'female',
      country: 'Canada'
    }),
    headers: {
      'Content-Type': 'application/json', 
       Authorization: test_user.token,
      }
  })

  // return email and password for logging in to newly created account
  return {
    email: email,
    password: password
  }

}

output.test_user = fillUserInfo()
```
