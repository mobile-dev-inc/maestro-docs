# Writing rules

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

{% hint style="info" %}
The mockserver folder **must** contain a file called `index.js` that serves as the root file of your rule definitions. You can then import other files containing other rules resulting in them also being applied.
{% endhint %}

### Writing rules

#### Defining a handler

<pre class="language-javascript"><code class="lang-javascript">// .maestro/mockserver/index.js

<strong>get('/endpoint', (req, res) => {
</strong>    res.json({
        message: 'Mocked by Maestro Mock Server'
    });
});
</code></pre>

The above snippet would return `{ message: 'Mocked by Maestro Mock Server' }` for all `GET` requests to the `/endpoint` . You can also mock the following request methods:

* `POST` is mocked by invoking the `post` method
* `PUT` is mocked by invoking the `put` method
* `PATCH` is mocked by invoking the `patch` method
* ... more HTTP methods coming soon!

{% hint style="info" %}
If you want to get started quickly with writing rules you can run `maestro mockserver init` to generate and deploy a sample rule for a GET request
{% endhint %}

```
type Handler = (req: Request, res: Response, session?: Session)

get(path: string, handler: Handler)
```

#### Configuring status code

You can chain a `.status()` call on the `res` object to control the status code being returned. The following example would return a `201` status code back to the client:

```javascript
// .maestro/mockserver/index.js

get('/endpoint', (req, res) => {
    res.status(201).json({
        message: 'Data created'
    });
});
```

If no status code is set, `200` will be used for mocked responses and for proxied requests that don't match any rule the original status code of the response will be used.

#### Returning a response to the client

You always need to call either `res.json()` or `res.text()` to signal to Maestro Mock Server that the response should be written back to the client, to avoid the request hanging.

### Using session

During the session, which is essentially tied to the app lifecycle, you can use the `session` object provided to your handler to keep state between requests. For example, if you want to simulate an authentication flow you can do that in the following way:

```javascript
// .maestro/mockserver/index.js

post('/login', (req, res, session) => {
    session.loggedIn = true   // The field name can be anything you want

    res.json({ message: 'success' });
});

get('/profile', (req, res, session) => {
    if (!session.loggedIn) {
        res.status(401).json({ message: 'Not logged in' });
    } else {
        res.json({ email: 'ada@lovelace.com' });
    }
});
```

### Using request propagation

Sometimes you want to gain access to the original data returned from your API and modify that on the way back to your client. In order to do that you can use request propagation and decorate your responses like this:

```javascript
// .maestro/mockserver/index.js

get('/endpoint', async (req, res, session) => {
    const originalRes = await req.propagate();
    const data = originalRes.json(); // you can also use .text() here
    
    res.json({ ...data, decorated: true });
});
```

The above example would return the same response as your backend with an additional field `decorated: true`.

### Using request body

If you want to access the original request body sent from your app you can do so through the `body` field on the request object. Note that it is passed as a string.

```javascript
// .maestro/mockserver/index.js

get('/endpoint', async (req, res, session) => {
    const body = JSON.parse(req.body);
    
    res.json({ originalBody: body });
});
```

### Deploying rules

Simply run `maestro mockserver deploy <path_to_your_mockserver_folder>` to deploy the rules.

{% hint style="warning" %}
Warning! Deploying your rules will override any other rules that other team members may have deployed. Maestro Mock Server always uses the latest deployed rules as a source of truth.
{% endhint %}
