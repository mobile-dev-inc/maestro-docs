# Matching Rules

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

Rules are stored in YAML files and follow the following format:

```yaml
# rules/myRule.yaml
- path: https://example.com             # URL that this rule matches
  method: POST                          # (optional) HTTP method. Default: GET
  headers:                              # (optional) Headers to match on
    Authorization: Bearer myToken 
  response:
    status: 500                         # (optional) HTTP response status code. Default: 200
    headers:                            # (optional) Response headers
        Content-Type: application/json
    # There are 2 ways to define a response body
    body: Hello World                   # (optiona) Text is returned back
    # OR
    bodyFile: myResponse.json           # (optional) Contents of the file are returned back

# Single YAML file can contain however many rules
- path: "https://example.com/.*"        # Path can contain regular expressions
  response:
    status: 401
```

### Matching

Matching is done by following principles:

* URL is matched first and needs to match exactly (or match a regular expression).
* If `headers` section is present.
  * All specified headers and their values have to be present in a request for it to match.
  * If an HTTP(s) request has extra headers that are not specified in the rule, the rule will still match as if those extra headers were not there.
* If `headers` section is not present then all requests headers will match (assuming that URL matched as well)
* Request body is not matched at the moment and is ignored.
* Matching stops at the first rule that fits the criteria. If you have multiple rules that match, only one of them will be used.
