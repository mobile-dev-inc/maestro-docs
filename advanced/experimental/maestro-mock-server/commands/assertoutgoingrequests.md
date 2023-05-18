# assertOutgoingRequests

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

{% hint style="info" %}
This command **requires the usage and setup of the Maestro Mock Server**, otherwise, it won't work. Please, check [its documentation page ](../)for more details.
{% endhint %}

The `assertOutgoingRequest` command was created so you can check if their app is properly doing requests to an API. With this command, you can check if the request is calling the right endpoint, check the HTTP headers, and so on.

Once you have Mock Server properly configured, all networks calls and rules can be seen with `maestro mockserver open`. Then, you can use `assertOutgoingRequest` command to check for API calls inside your Flow.

Here is an example of the command usage. The `path` property is **required**, but all others are optional. Also, note that it's possible to regex in all property values.

```
- assertOutgoingRequest:
    path: "/login" # required
    headersPresent: #optional
      - "cache-control"
    headersAndValues: #optional
      - "Content-Type": "*application/json*"
      - "Authorization": "Bearer .*"
    httpMethodIs: "GET" # optional
    requestBodyContains: '"foo": "bar"' # optional
```

Description of each option:

* **path** (required): Assert for the API URI called. You can use a string to assert if it's equal or a regex. Note that you should not specify the base URL of the backend (that you already did with Maestro SDK). Example: if the complete URL is `https://example.com/foo/bar`, you will use only `/foo/bar`
* **headersPresent** (optional)**:** Check if all items of the list provided headers are present (regardless of their value) in the request headers. You can use regex here too.
* **headersAndValues** (optional)**:** Check if the specified HTTP headers contain the declared value. You can also use regex to check for the header value.
* **httpMethodIs** (optional)**:** Check which  HTTP method is used in the request.
* **requestBodyContains** (optional)**:** Check if the body of the request contains the right content. You can use regex to check for the value.
