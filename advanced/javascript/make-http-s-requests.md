# Make HTTP(s) requests

Maestro comes with its own JavaScript HTTP API

```javascript
// script.js
const response = http.get('https://example.com')

output.script.result = response.body
```

### JSON

Use `json()` function to parse JSON responses.&#x20;

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
    body: JSON.stringify(
        {
            myField: "Payload"
        }
    )
})
```

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

| Field Name | Value                                               |
| ---------- | --------------------------------------------------- |
| `ok`       | `true` if request was successful, `false` otherwise |
| `status`   | HTTP status code (i.e. `200`)                       |
| `body`     | String body of the response                         |
