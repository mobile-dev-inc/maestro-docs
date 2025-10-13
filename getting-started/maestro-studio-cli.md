---
description: >-
  Write Maestro flows faster with Studio in the CLI. Visually pick UI elements,
  get auto-generated YAML examples, and run commands inline.
---

# Maestro Studio (CLI)

{% embed url="https://youtu.be/g6HaT6CzUrk" %}

Use Maestro Studio to instantly discover the exact commands needed to interact with your app.

Here’s how it works:

### Launch Maestro Studio <a href="#b415" id="b415"></a>

Maestro Studio is built right into the Maestro CLI. Upgrade your CLI to the latest version, and run the command below to launch Maestro Studio in your browser:

```bash
maestro studio
```

Here’s what you’ll see:

<figure><img src="../.gitbook/assets/Screenshot 2023-07-13 at 18.54.53.png" alt=""><figcaption></figcaption></figure>

You can either visually select UI elements in order to receive suggestions on how to interact with the element in your Flow, or enter Maestro commands in the REPL and run them by pressing `Run`.

### Visually Select a UI Element <a href="#id-2508" id="id-2508"></a>

Click on the device screenshot to select a UI element, e.g. Settings icon on the iOS simulator.

<figure><img src="../.gitbook/assets/Screenshot 2023-07-13 at 18.58.06.png" alt=""><figcaption></figcaption></figure>

#### Automatically Generated Examples <a href="#id-725d" id="id-725d"></a>

Maestro Studio automatically generates examples of how you can interact with the selected element in your Flows. You can double click on the example to execute it directly, or use the hotkeys to copy it to the clipboard or open the relevant documentation.

### Executing commands in the REPL

You can execute Maestro commands inline in Studio in the REPL view. The commands are written in YAML in the same way as you would write any normal Flow.

<figure><img src="../.gitbook/assets/Screenshot 2023-07-17 at 19.12.37.png" alt=""><figcaption></figcaption></figure>
