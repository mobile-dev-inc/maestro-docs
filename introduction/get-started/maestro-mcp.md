---
description: >-
  Use Maestro's MCP server to let your coding agent write, run, and debug mobile
  and web UI tests.
---

# Maestro MCP Server

Maestro implements the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro), enabling direct integration coding agents like Claude Code, Claude Desktop, Cursor, GitHub Copilot, Codex, Codex Desktop, Gemini, Windsurf, and JetBrains AI Assistant ([full list](https://modelcontextprotocol.io/clients)). For more information on MCP see [#what-is-mcp](maestro-mcp.md#what-is-mcp "mention").

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FCbCMt5C3rawmE9oIus7f%2Fuploads%2FmkNE7cEla6mI7Ikp0aH5%2Fmaestro-mcp.mp4?alt=media&token=b63eb192-ce07-4614-878c-69cf447eae2e" %}

## How to Install Maestro MCP

{% stepper %}
{% step %}
### Prerequisites

* Install [Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli)
* Any coding agent that supports MCP ([full list](https://modelcontextprotocol.io/clients))
{% endstep %}

{% step %}
### Install the Maestro MCP on your coding agent

<details>

<summary><i class="fa-claude">:claude:</i>  Claude Code CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  Run:

    ```bash
    claude mcp add maestro -- maestro mcp
    ```

{% hint style="info" %}
See the [Claude Code MCP docs](https://docs.claude.com/en/docs/claude-code/mcp) for scope options (`--scope user`, `--scope project`, etc.).
{% endhint %}

</details>

<details>

<summary><i class="fa-chatgpt">:chatgpt:</i>  Codex CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  Run:

    ```bash
    codex mcp add maestro -- maestro mcp
    ```

    Or add to `~/.codex/config.toml` manually:

    ```toml
    [mcp_servers.maestro]
    command = "maestro"
    args = ["mcp"]
    ```

See the [Codex MCP docs](https://developers.openai.com/codex/mcp) and the [config reference](https://developers.openai.com/codex/config-reference).

</details>

<details>

<summary><i class="fa-chatgpt">:chatgpt:</i>  Codex Desktop App</summary>

The Codex Desktop App shares its MCP config (`~/.codex/config.toml`) with the Codex CLI. If Maestro is already set up there, the Desktop App will pick it up automatically.

Otherwise:

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. In the Codex Desktop App, click the **Settings** button, then **Settings** again, and select **MCP servers** in the sidebar.
3.  Click **Add server** and fill in the form:

    * **Name:** `maestro`
    * **Type:** `STDIO`
    * **Command to launch:** `maestro`
    * **Arguments:** `mcp`

    Then click **Save**.

See the [Codex MCP docs](https://developers.openai.com/codex/mcp) and the [config reference](https://developers.openai.com/codex/config-reference).

</details>

<details>

<summary><i class="fa-claude">:claude:</i>  Claude Desktop</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  In Claude Desktop, open **Settings → Developer → Edit Config** and merge the following into `claude_desktop_config.json`:

    ```json
    {
        "mcpServers": {
            "maestro": {
                "command": "<full path to maestro binary>",
                "args": ["mcp"],
                "env": {
                    "JAVA_HOME": "<full JAVA_HOME directory>"
                }
            }
        }
    }
    ```

    The config file lives at:

    * **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
    * **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

    Claude Desktop launches from a minimal shell, so pass `JAVA_HOME` explicitly and use the full path to the `maestro` binary (run `which maestro` in your terminal to find it).

{% hint style="info" %}
The **Connectors** UI in Claude Desktop only supports remote MCP servers that use OAuth. Local stdio servers like Maestro must be added by editing `claude_desktop_config.json` directly.
{% endhint %}

</details>

<details>

<summary><i class="fa-github">:github:</i>  GitHub Copilot CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  In a Copilot CLI session, run `/mcp add` and follow the interactive form with:

    * Name: `maestro`
    * Type: `local`
    * Command: `maestro mcp`

    Or add to `~/.copilot/mcp-config.json` manually:

    ```json
    {
        "mcpServers": {
            "maestro": {
                "type": "local",
                "command": "maestro",
                "args": ["mcp"]
            }
        }
    }
    ```

See the [Copilot CLI MCP docs](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers).

</details>

<details>

<summary><i class="fa-cursor">:cursor:</i>  Cursor IDE</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  Install the MCP. The quickest option is the one-click button:

    [![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en-US/install-mcp?name=maestro\&config=eyJjb21tYW5kIjoibWFlc3RybyBtY3AifQ%3D%3D)

    Or set it up manually: open **Cursor Settings → Tools & MCPs → Add Custom MCP**. Cursor opens `~/.cursor/mcp.json` for editing. Merge the following into it (or into a project-scoped `.cursor/mcp.json` in your repo root):

    ```json
    {
        "mcpServers": {
            "maestro": {
                "command": "maestro",
                "args": ["mcp"]
            }
        }
    }
    ```

See the [Cursor MCP docs](https://cursor.com/docs/context/mcp) for more.

</details>

<details>

<summary><i class="fa-cursor">:cursor:</i>  Cursor CLI</summary>

The Cursor CLI shares its MCP config with the Cursor IDE. If Maestro is already set up in the IDE, there's nothing else to do.

Otherwise:

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  Add Maestro to `.cursor/mcp.json` in your project root:

    ```json
    {
        "mcpServers": {
            "maestro": {
                "command": "maestro",
                "args": ["mcp"]
            }
        }
    }
    ```

See the [Cursor CLI MCP docs](https://cursor.com/docs/cli/mcp).

</details>

<details>

<summary><i class="fa-google">:google:</i>  Gemini CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2.  Run:

    ```bash
    gemini mcp add maestro maestro mcp
    ```

    Or add to `~/.gemini/settings.json` manually:

    ```json
    {
        "mcpServers": {
            "maestro": {
                "command": "maestro",
                "args": ["mcp"]
            }
        }
    }
    ```

{% hint style="info" %}
See the [Gemini CLI MCP docs](https://geminicli.com/docs/tools/mcp-server/) for scope options (`-s user`, `-s project`, etc.).
{% endhint %}

</details>

<details>

<summary><i class="fa-rectangle-terminal">:rectangle-terminal:</i>  Other Coding Agents / Manual Installation</summary>

If your agent isn't listed above, the generic stdio config is:

```json
{
    "mcpServers": {
        "maestro": {
            "command": "maestro",
            "args": ["mcp"]
        }
    }
}
```

{% hint style="info" %}
This assumes `maestro` is on your `PATH`. If it isn't, replace `"maestro"` with the full path to the Maestro CLI executable (e.g. `/opt/homebrew/bin/maestro`).
{% endhint %}

If you run into PATH or JAVA\_HOME issues, you can specify them explicitly:

```json
{
    "mcpServers": {
        "maestro": {
            "command": "<full path to maestro binary>",
            "args": ["mcp"],
            "env": {
                "JAVA_HOME": "<full JAVA_HOME directory>"
            }
        }
    }
}
```

MCP documentation for other IDEs:

* [Windsurf](https://docs.windsurf.com/windsurf/cascade/mcp)
* [JetBrains IDEs](https://www.jetbrains.com/help/ai-assistant/configure-an-mcp-server.html)
* [VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server)

</details>
{% endstep %}

{% step %}
### Restart and start building

Restart your coding agent, then let your agent handle checking its own work against a live mobile emulator or simulator. And when you're ready, generate repeatable end to end tests to ensure your feature doesn't break going forward.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

## How to Use the Maestro Viewer

Maestro MCP ships with Maestro Viewer - a web app that embeds an iOS simulator or Android emulator or physical device into your coding agent or browser. It shows the exact commands that Maestro MCP runs in real time, and enables full interactions with the embedded mobile device, allowing you to iterate end to end completely within the coding agent app of your choice.

The Maestro Viewer is exposed via the `open_maestro_viewer`  MCP tool, so to open it simply ask your coding agent:

> open the maestro viewer

Here's an example of the Maestro Viewer running in the embedded Cursor IDE browser:

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FCbCMt5C3rawmE9oIus7f%2Fuploads%2F2eQdX7WY0CrBEJ8iIOr3%2Fmaestro-viewer.mp4?alt=media&token=a063e0d0-5e0c-41ab-8415-f253e96f64dc" %}

## How to Update Maestro MCP

The Maestro MCP is bundled inside the Maestro CLI, so upgrading the CLI upgrades the MCP server. After upgrading, your agent needs to reload the MCP connection to pick up the new binary.

{% stepper %}
{% step %}
### Update the Maestro CLI

Maestro MCP ships as part of the Maestro CLI, so to update Maestro MCP:

* [Update the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli/update-the-maestro-cli)
{% endstep %}

{% step %}
### Reload the Maestro MCP in your coding agent

<details>

<summary><i class="fa-claude">:claude:</i>  Claude Code CLI</summary>

Run `/mcp`, select **maestro**, then **Reconnect**.

</details>

<details>

<summary><i class="fa-claude">:claude:</i>  Claude Desktop</summary>

Restart Claude Desktop.

</details>

<details>

<summary><i class="fa-chatgpt">:chatgpt:</i>  Codex CLI</summary>

Restart the Codex CLI.

</details>

<details>

<summary><i class="fa-chatgpt">:chatgpt:</i>  Codex Desktop App</summary>

Restart the Codex Desktop App.

</details>

<details>

<summary><i class="fa-github">:github:</i>  GitHub Copilot CLI</summary>

Restart the Copilot CLI.

</details>

<details>

<summary><i class="fa-cursor">:cursor:</i>  Cursor IDE</summary>

**Cursor Settings → Tools & MCPs** and toggle the Maestro server off and on, or restart Cursor.

</details>

<details>

<summary><i class="fa-cursor">:cursor:</i>  Cursor CLI</summary>

Restart `cursor-agent`. No in-session reload command exists.

</details>

<details>

<summary><i class="fa-google">:google:</i>  Gemini CLI</summary>

Restart the Gemini CLI.

</details>

<details>

<summary><i class="fa-rectangle-terminal">:rectangle-terminal:</i>  Other Coding Agents</summary>

Restart your coding agent.

</details>
{% endstep %}
{% endstepper %}

## MCP tools

| Tool                   | Description                                                                                                                                                                                                                 |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `list_devices`         | List all available local devices (Android emulators, iOS simulators, and Chromium for web) that can be targeted for automation.                                                                                             |
| `inspect_screen`       | Get the current screen's view hierarchy as compact JSON. Call this before targeting elements, and re-call after any UI change.                                                                                              |
| `take_screenshot`      | Take a screenshot of the current device screen. Useful when a visual helps disambiguate elements.                                                                                                                           |
| `run`                  | Execute Maestro flows. Accepts exactly one of `{ yaml }` (inline YAML, preferred for exploration), `{ files }` (specific `.yaml` files), or `{ dir, include_tags, exclude_tags }`. Syntax is validated as part of the call. |
| `cheat_sheet`          | Return the Maestro cheat sheet covering common commands, flow syntax, and best practices. The agent should call this before authoring unfamiliar commands.                                                                  |
| `list_cloud_devices`   | List valid `{ device_model, device_os }` pairs available on Maestro Cloud. Call before `run_on_cloud`. OS versions must be passed verbatim (e.g. `iOS-17-5`, `android-34`).                                                 |
| `run_on_cloud`         | Submit a flow (or folder of flows) to Maestro Cloud. Returns `upload_id`, `project_id`, and a dashboard URL immediately.                                                                                                    |
| `get_cloud_run_status` | Poll the status and per-flow results of a Cloud run. Poll every 60s until the status is terminal (`SUCCESS`, `ERROR`, `CANCELED`, `WARNING`).                                                                               |
| `open_maestro_viewer`  | Returns the running Viewer URL.                                                                                                                                                                                             |

{% hint style="info" %}
The `list_cloud_devices`, `run_on_cloud`, and `get_cloud_run_status` tools require Maestro Cloud authentication. Run `maestro login` (recommended) or set `MAESTRO_CLOUD_API_KEY` for non-interactive environments.
{% endhint %}

## What is MCP?

The Model Context Protocol is an open standard that provides a uniform interface for connecting Large Language Models to external data sources, tools, and services. MCP defines a client-server architecture where:

* **MCP Servers** expose resources like data sources, APIs, and tools through a standardized interface.
* **MCP Clients**, such as AI apps, consume these resources via the protocol.
* **Transport Layer** handles communication using JSON-RPC 2.0 over stdio, HTTP with Server-Sent Events (SSE), or WebSocket connections.

The Maestro MCP server ships inside the Maestro CLI and exposes Maestro's authoring, device, and Cloud capabilities to your agent over stdio.
