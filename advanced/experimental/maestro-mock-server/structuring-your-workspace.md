# Structuring your workspace

{% hint style="danger" %}
This is a deprecated feature that will be removed in a future version of Maestro.
{% endhint %}

## Separating your rules in different files

You can structure your rules in different files for organization and then add imports to your other modules from your `index.js` file. The following example shows how to import all rules defined in `auth.js` - note that importing them is enough.

```javascript
// .maestro/mockserver/index.js

import "./auth.js";

get('/endpoint', (req, res) => {
    res.json({
        message: 'Mocked by Maestro Mock Server'
    });
});
```

```javascript
// .maestro/mockserver/auth.js

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

## Modules and imports

If you want to import normal JavaScript functions from other modules you can use normal module behaviour for imports and exports

```javascript
// .maestro/mockserver/index.js

import { sum } from './helpers.js';
  
get('/endpoint', (req, res) => {
    res.json({
        message: 'Mocked by Maestro Mock Server',
        result: sum(1, 2)
    });
});
```

```javascript
// .maestro/mockserver/helpers.js

export const sum = (a, b) => a + b;
```
