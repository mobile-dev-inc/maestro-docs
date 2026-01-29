# Maestro MCP Server

Maestro implements the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro), enabling direct integration with MCP-compliant client apps such as Claude, Cursor, and Windsurf.

The Model Context Protocol is an open standard that provides a uniform interface for connecting Large Language Models to external data sources, tools, and services. MCP defines a client-server architecture where:

* **MCP Servers** expose resources like data sources, APIs, and tools through a standardized interface
* **MCP Clients**, such as AI apps, consume these resources via the protocol
* **Transport Layer** handles communication using JSON Remote Procedure Call (RPC) 2.0 over stdio, HTTP with Server-Sent Events (SSE), or WebSocket connections

This architectural pattern decouples LLMs from specific integrations, allowing Maestro to function as an MCP server that exposes its capabilities through a protocol-defined interface rather than requiring custom SDK implementations for each client.

## Prerequisites

To install and use the Maestro MCP server, you need the following:

* Maestro command-line tool installed
* An IDE compatible with MCP servers

## Install the Maestro MCP server

To install the Maestro MCP server, on your terminal, run `maestro mcp`

The Maestro command-line tool preinstalls the MCP server, so this is enough to install.

## Configure the MCP server on your IDE

Most IDEs have a `json` configuration file to indicate to IDE how to run the MCP server. To do this, open your MCP configuration file. For example, if you're using Claude Desktop, it is `~/Library/Application Support/Claude/claude_desktop_config.json` on macOS or `%APPDATA%\Claude\claude_desktop_config.json` on Windows. For VSCode, edit the `.vscode/mcp.json` for your workspace.

The `json` configuration file for Maestro MCP serve is:

```json
{
    "mcpServers": {
        "maestro": {
            "command": "maestro",
            "args": [
                "mcp"
            ]
        }
    }
}
```

{% hint style="info" %}
Assumes Maestro CLI is installed and available on your PATH. If it's not on your PATH, use the full path to the Maestro CLI executable instead of `maestro`.
{% endhint %}

**For other IDEs and more information, consult their documentation:**

* [Windsurf](https://docs.windsurf.com/windsurf/mcp#adding-a-new-server)
* [Cursor](https://docs.cursor.com/context/model-context-protocol#configuring-mcp-servers)
* [VSCode](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server)
* [JetBrains IDEs](https://www.jetbrains.com/help/ai-assistant/configure-an-mcp-server.html)

## MCP commands

| Command                  | Description                                                            |
| ------------------------ | ---------------------------------------------------------------------- |
| `back`                   | Press the back button.                                                 |
| `cheat_sheet`            | Get the Maestro cheat sheet with common commands and syntax examples.  |
| `check_flow_syntax`      | Validates the syntax of a flow.                                        |
| `input_text`             | Input text to the current focused text field.                          |
| `inspect_view_hierarchy` | Get the nested views hierarchy of the current screen in CSV format.    |
| `launch_app`             | Launch an app on the connected device.                                 |
| `list_devices`           | List all devices.                                                      |
| `query_docs`             | Query the Maestro documentation for specific information.              |
| `run_flow`               | Run a flow.                                                            |
| `run_flow_files`         | Run one or more full Maestro flows.                                    |
| `start_device`           | Start a device like a simulator or emulator and returns the device ID. |
| `stop_app`               | Stop an app on the connected device.                                   |
| `take_screenshot`        | Take a screenshot of the current device screen.                        |
| `tap_on`                 | Tap on a UI element using the selector description.                    |
