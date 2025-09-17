---
description: How to use NPM packages in Maestro's runScript command
---

# Using NPM Packages in runScript

With [runScript](../../api-reference/commands/runscript.md) Maestro allows you to run a JavaScript file. However the support is very limited due to the used JavaScript engine. For example you cannot use `import` or `require` statements to include NPM packages.

That's why [Paradiesvogel7](https://github.com/Paradiesvogel7) came up with a clever solution. The idea is to bundle and compile the JavaScript code along with its dependencies into a single file that can be executed with [GraalJS](https://github.com/oracle/graaljs).

{% hint style="info" %}
Note: Since Maestro v2, GraalJS is the default JavaScript engine. If you are using an older version, please refer to [GraalJS support](../javascript/graaljs-support.md) to learn how to enable it.
{% endhint %}

To achieve this, you can use a tools like [webpack](https://webpack.js.org/) and [babel](https://babeljs.io/). Below is an example configuration that demonstrates how to set this up.

```javascript
// generateTotp.js
const OTPAuth = require('otpauth');

const defaultOptions = {
  algorithm: 'SHA1',
  digits: 6,
  period: 30
};

function generateTotp() {
  const secret = MAESTRO_TOTP_SECRET;
  if (!secret) throw new Error('OTP secret is required.');

  const totp = new OTPAuth.TOTP({
    ...defaultOptions,
    secret: OTPAuth.Secret.fromBase32(secret)
  });

  return totp.generate();
}

output.totp = generateTotp();
```


```javascript
// webpack.config.js
const path = require('path');

module.exports = {
  entry: './generateTotp.js',
  output: {
    path: path.resolve(__dirname, 'lib'),
    filename: 'generateTotp.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader'
      }
    ]
  },
  mode: 'production'
};
```

Now to be able to run the code above, you need to run webpack before executing your Maestro flow.

```bash
webpack --config webpack.config.js
```

Finally, you can use the bundled JavaScript file in your Maestro flow like this:

```yaml
# Example flow using the bundled JavaScript file
appId: com.example.app
---
- tapOn: "Code"
- runScript: ./lib/generateTotp.js
- inputText: ${output.totp}
- tapOn: "Verify"
```