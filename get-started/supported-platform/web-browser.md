# Web Browsers

Maestro extends its one framework to rule them all philosophy to the desktop browser. By using the same declarative YAML syntax you use for mobile, you can automate web applications, enabling unified end-to-end testing across your entire product surface.

{% hint style="warning" %}
#### Beta Status

Web support is currently in Beta. It is functional for Chromium-based testing and is ideal for teams looking to consolidate their mobile and web automation into a single toolset.
{% endhint %}

### Technical approach

Maestro maintains its "Arm's Length" philosophy for web testing. Instead of directly manipulating the DOM or injecting JavaScript, Maestro interacts with the browser as a user would.

* **Unified Syntax**: The same commands like `tapOn`, `inputText`, and `assertVisible` work identically on Web as they do on Android and iOS.
* **Framework Agnostic**: Whether your site is built with React, Vue, Angular, or plain HTML, Maestro interacts with the rendered output.

### Execution Workflow

For web tests, you replace the `appId` with a `url`. Behind the scenes, Maestro treats the URL as the unique identifier for the application session.

```yaml
# example.yaml
url: https://maestro.mobile.dev
---
- launchApp
- tapOn: "Installing Maestro"
- assertVisible: "Installing the CLI"
```

On the first run, Maestro will automatically download a managed version of Chromium. Subsequent runs will launch instantly. To run the test with [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/), just run:

```bash
maestro test example.yaml
```

### Maestro Studio for Web

[Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/) is fully compatible with web testing. It allows you to visually inspect web elements and generate YAML commands through a point-and-click interface.&#x20;

### Platform specifics and tips

* **Flutter Web**: Just like Flutter Mobile, Flutter Web renders elements differently. You should use Semantics to make elements addressable. Refer to the [Flutter](https://docs.maestro.dev/platform-support/flutter) documentation for best practices.
* [**Selectors**](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/how-to-use-selectors): Maestro prioritizes user-visible text. For complex web apps, using unique text labels or stable accessibility attributes is recommended to ensure your tests remain "refactoring resilient."

### Known limitations

As this feature is in Beta, certain advanced browser configurations are not yet supported:

* **Browser Engines**: The current default and only supported browser is Chromium.
* **Localization**: The default locale is set to `en-US`.
* **Screen Dimensions**: Custom screen size and viewport configuration are currently preset.

### Next steps

If you don't know how to create tests with Maestro, access the [Quickstart](../quickstart.md) guide to get up and running in minutes.

To learn how to create tests, refer to the [Flows](https://app.gitbook.com/s/mS3lsb9jRwfRHqddeRXG/) documentation. If you want to explore Maestro solutions, consult the appropriate documentation:

* [Maestro Studio](https://app.gitbook.com/s/eQi66gxHTt2vx4HjhM9V/)
* [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/)
* [Maestro Cloud](https://app.gitbook.com/s/ky7LkNoLfvcORtXOzzBs/)
