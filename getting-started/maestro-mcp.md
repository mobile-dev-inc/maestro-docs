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

The MCP command comes pre-installed as part of the Maestro CLI - you can run it with `maestro mcp`


## Configuring your MCP Client

Configuration varies depending on the MCP Client you are using. 

### Claude Desktop

For Claude, you can follow the instructions in the [Claude documentation](https://modelcontextprotocol.io/quickstart/user).

The configuration file is typically located at `~/Library/Application Support/Claude/claude_desktop_config.json` on OSX or `%APPDATA%\Claude\claude_desktop_config.json` on Windows. Add the following configuration to the file and restart Claude:

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

Replace `maestro` with the full path of your maestro cli, if not on path.

Other clients have similar configuration files and the installation processs may vary. Please follow their specific installation instructions:

- [Windsurf](https://docs.windsurf.com/windsurf/mcp#adding-a-new-server)
- [Cursor](https://docs.cursor.com/context/model-context-protocol#configuring-mcp-servers)
- [VSCode](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server)

