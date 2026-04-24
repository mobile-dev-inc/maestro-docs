---
description: >-
  Use Maestro's Model Context Protocol (MCP) server to let your coding agent
  write, run, and debug mobile and web UI tests.
---

# Maestro MCP Server

Maestro implements the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro), enabling direct integration with MCP-compliant coding agents such as Claude Code, Claude Desktop, Cursor, GitHub Copilot, Codex, Gemini, Windsurf, and JetBrains AI Assistant.

The Model Context Protocol is an open standard that provides a uniform interface for connecting Large Language Models to external data sources, tools, and services. MCP defines a client-server architecture where:

* **MCP Servers** expose resources like data sources, APIs, and tools through a standardized interface.
* **MCP Clients**, such as AI apps, consume these resources via the protocol.
* **Transport Layer** handles communication using JSON-RPC 2.0 over stdio, HTTP with Server-Sent Events (SSE), or WebSocket connections.

The Maestro MCP server ships inside the Maestro CLI and exposes Maestro's authoring, device, and Cloud capabilities to your agent over stdio.

## Prerequisites

* The [Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli) installed and available on your `PATH`.
* A coding agent that supports MCP (see the install paths below).

## Install the Maestro MCP server on your coding agent

Installing the Maestro MCP takes two steps:

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli) (via the curl script or Homebrew).
2. Register the Maestro MCP with your coding agent, using either the agent's one-line install command or a manual JSON/TOML config.

If your agent isn't listed below, the generic stdio config is:

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

<details>

<summary>Claude Code CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. Run:

    ```bash
    claude mcp add maestro -- maestro mcp
    ```

{% hint style="info" %}
See the [Claude Code MCP docs](https://docs.claude.com/en/docs/claude-code/mcp) for scope options (`--scope user`, `--scope project`, etc.).
{% endhint %}

</details>

<details>

<summary>Codex</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. Run:

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

<summary>Claude Desktop</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. In Claude Desktop, open **Settings → Developer → Edit Config** and merge the following into `claude_desktop_config.json`:

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

<summary>GitHub Copilot CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. In a Copilot CLI session, run `/mcp add` and follow the interactive form with:

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

<summary>Cursor IDE</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. Open **Cursor Settings → Tools & MCPs → Add Custom MCP**. Cursor opens `~/.cursor/mcp.json` for editing. Merge the following into it (or into a project-scoped `.cursor/mcp.json` in your repo root):

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

<summary>Cursor CLI</summary>

The Cursor CLI shares its MCP config with the Cursor IDE. If Maestro is already set up in the IDE, there's nothing else to do.

Otherwise:

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. Add Maestro to `.cursor/mcp.json` in your project root:

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

<summary>Gemini CLI</summary>

1. [Install the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli).
2. Run:

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

**For other IDEs, use the generic stdio config above and consult their documentation:**

* [VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server)
* [JetBrains IDEs](https://www.jetbrains.com/help/ai-assistant/configure-an-mcp-server.html)
* [Windsurf](https://docs.windsurf.com/windsurf/cascade/mcp)

## Update the Maestro MCP server

The Maestro MCP is bundled inside the Maestro CLI, so upgrading the CLI upgrades the MCP server. After upgrading, your agent needs to reload the MCP connection to pick up the new binary.

1. [Update the Maestro CLI](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli/update-the-maestro-cli).
2. Reload the Maestro MCP in your agent:

| Agent                | How to reload                                                                  |
| -------------------- | ------------------------------------------------------------------------------ |
| Claude Code CLI      | Run `/mcp`, select **maestro**, then **Reconnect**.                            |
| Codex                | Restart the Codex CLI.                                                         |
| Claude Desktop       | Restart Claude Desktop.                                                        |
| GitHub Copilot CLI   | Restart the Copilot CLI.                                                       |
| Cursor IDE           | **Cursor Settings → Tools & MCPs** and toggle the Maestro server off and on, or restart Cursor. |
| Cursor CLI           | Restart `cursor-agent`. No in-session reload command exists.                   |
| Gemini CLI           | Restart the Gemini CLI.                                                        |

## MCP tools

| Tool                   | Description                                                                                                                                                                                              |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `list_devices`         | List all available local devices (Android emulators, iOS simulators, and Chromium for web) that can be targeted for automation.                                                                           |
| `inspect_screen`       | Get the current screen's view hierarchy as compact JSON. Call this before targeting elements, and re-call after any UI change.                                                                            |
| `take_screenshot`      | Take a screenshot of the current device screen. Useful when a visual helps disambiguate elements.                                                                                                         |
| `run`                  | Execute Maestro flows. Accepts exactly one of `{ yaml }` (inline YAML, preferred for exploration), `{ files }` (specific `.yaml` files), or `{ dir, include_tags, exclude_tags }`. Syntax is validated as part of the call. Replaces the old `run_flow` + `run_flow_files` pair and the imperative single-action tools. |
| `cheat_sheet`          | Return the Maestro cheat sheet covering common commands, flow syntax, and best practices. The agent should call this before authoring unfamiliar commands.                                                |
| `list_cloud_devices`   | List valid `{ device_model, device_os }` pairs available on Maestro Cloud. Call before `run_on_cloud`. OS versions must be passed verbatim (e.g. `iOS-17-5`, `android-34`).                                |
| `run_on_cloud`         | Submit a flow (or folder of flows) to Maestro Cloud. Returns `upload_id`, `project_id`, and a dashboard URL immediately.                                                                                  |
| `get_cloud_run_status` | Poll the status and per-flow results of a Cloud run. Poll every 60s until the status is terminal (`SUCCESS`, `ERROR`, `CANCELED`, `WARNING`).                                                             |

{% hint style="info" %}
The `list_cloud_devices`, `run_on_cloud`, and `get_cloud_run_status` tools require Maestro Cloud authentication. Run `maestro login` (recommended) or set `MAESTRO_CLOUD_API_KEY` for non-interactive environments.
{% endhint %}
