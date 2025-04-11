# Model Context Protocol (MCP)

Maestro supports the [MCP protocol](https://modelcontextprotocol.io/), which allows it to be used directly by any MCP Client tools (such as Claude, Cursor or Windsurf).

## What is MCP?

Model Context Protocol (MCP) is a standardized protocol that bridges AI models with various data sources and tools. Think of it as the "USB-C for AI" — a universal connector that enables seamless communication between large language models (LLMs) and the resources they need.

### Why MCP Matters

MCP solves three critical challenges in AI integration:

1. **Universal Connectivity**: Provides a single protocol for connecting AI systems to diverse data sources and tools
2. **Vendor Independence**: Allows easy switching between different LLM providers without changing integrations
3. **Secure Access**: Implements best practices for safely accessing data within organizational boundaries

### How MCP Works

MCP uses a simple but powerful architecture:

- **MCP Hosts**: Applications (like IDEs or AI assistants) that need access to data through MCP
- **MCP Clients**: Protocol handlers that connect hosts to servers
- **MCP Servers**: Specialized programs that expose capabilities through the standardized protocol
- **Data Sources**: Local files, databases, and services that MCP can securely access
- **External Services**: Remote systems (APIs, etc.) that MCP servers can connect to


## Installing Maestro MCP

### Make sure Python 3.11 is in use

[Maestro MCP](https://github.com/mobile-dev-inc/maestro-mcp) is distributed in the form of a [Python package](https://github.com/mobile-dev-inc/maestro-mcp). It requires the latest Maestro cli and Python 3.11+ to function correctly. Verify the python version you have with:

```
python --version
```

If you don't have Python 3.11 or higher, you can install it with tools such as Anaconda, Pyenv or downloading Python directly.

### Install the latest Maestro CLI

Follow the [Maestro CLI](../getting-started/installing-maestro) installation instructions as usual. Maestro MCP requires the latest Maestro cli to function correctly.


### Installing Maestro MCP

Install Maestro MCP with:

```bash
pip install maestro-mcp
```

You can now use it on any MCP Client of your choice.


## Configuring your MCP Client

Configuration varies depending on the MCP Client you are using. 

### Claude Desktop

For Claude, you can follow the instructions in the [Claude documentation](https://modelcontextprotocol.io/quickstart/user).

The configuration file is typically located at `~/Library/Application Support/Claude/claude_desktop_config.json` on OSX or `%APPDATA%\Claude\claude_desktop_config.json` on Windows. Add the following configuration to the file and restart Claude:

```json
{
  "mcpServers": {
    "maestro": {
      "command": "python",
      "args": [
        "-m",
        "maestro_mcp.cli"
      ]
    }
  }
}
```

If you have more than one Python installation, you might have to specify the full path to your python installation. 

For example, if you're using pyenv on OSX, you might need to use `/Users/<your user>/.pyenv/versions/3.11.10/bin/python` instead of `python` on the `command` field above.

Other clients have similar configuration files and the installation processs may vary. Please follow their specific installation instructions:

- [Windsurf](https://docs.windsurf.com/windsurf/mcp#adding-a-new-server)
- [Cursor](https://docs.cursor.com/context/model-context-protocol#configuring-mcp-servers)
- [VSCode](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server)

