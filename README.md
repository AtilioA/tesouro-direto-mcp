[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/atilioa-tesouro-direto-mcp-badge.png)](https://mseep.ai/app/atilioa-tesouro-direto-mcp)

# Tesouro Direto MCP Server

[![npm version](https://img.shields.io/npm/v/tesouro-direto-mcp.svg)](https://www.npmjs.com/package/tesouro-direto-mcp)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](LICENSE)

A Model Context Protocol (MCP) server implementation for integrating with the Tesouro Direto API, enabling natural language access to Brazilian treasury bond data.

---

## Features

Query market data, bond details, and search/filter bonds using everyday language through MCP-compatible clients.

- **MCP tools**:
  - `market_data`: Retrieve general treasury bond market data (opening/closing times, status)
  - `bond_data`: Get detailed information about a specific bond
  - `search_bonds`: Search/filter bonds by type, maturity, and other criteria
- **Smart caching**: 10-minute in-memory cache based on API update timestamps to reduce calls while ensuring data freshness.

---

## Example usage

In a MCP-compatible client, you can use the following prompts:

- *"Show all available Tesouro Direto bonds"*
- *"Get details for the bond IPCA+ 2029"*
- *"Search for IPCA bonds maturing after 2045"*
- *"What is the current treasury bond market status?"*
- *"Provide a detailed analysis of the top three bonds with the highest yields for both IPCA and fixed-rate bonds."*

---

## Installation

### Installing via npm

### Example JSON for MCP client configuration (Cursor/Claude)

With [npx](https://docs.npmjs.com/cli/commands/npx), add this to your `~/.cursor/mcp.json`, or `claude_desktop_config.json` if you are using its desktop app:

```json
{
    "mcpServers": {
        "tesouro-direto": {
            "command": "npx",
            "args": [
                "-y",
                "tesouro-direto-mcp"
            ],
            "env": {
                "USE_MCP_CACHE": "true"
            }
        }
    }
}
```

---

### Building from source

```bash
# Clone the repository
git clone https://github.com/AtilioA/tesouro-direto-mcp.git
cd tesouro-direto-mcp

# Install dependencies
pnpm install

# Build the project
pnpm run build
```

You can run the MCP server directly after building:

```bash
node dist/index.js
```

Or use it with any MCP-compatible client (e.g., MCP Inspector):

```bash
npx @modelcontextprotocol/inspector dist/index.js
```

---

## Tools

### `market_data`

Retrieve general market data, including opening/closing times and current status.

### `bond_data`

Get detailed information for a specific bond by its code.

### `search_bonds`

Search and filter bonds by type (SELIC, IPCA, PREFIXADO), maturity date, and more.

---

## Environment variables

| Variable         | Description                                 | Default |
|------------------|---------------------------------------------|---------|
| `USE_MCP_CACHE`  | Enable the in-memory cache for API responses| `true`  |

Set these in your environment or in your MCP client configuration.

---

## Project structure

```
src/
├── api/         # API client for Tesouro Direto
│   └── tesouroDireto.ts
├── cache/       # Caching implementation
│   └── apiCache.ts
├── resources/   # MCP resources implementation
│   └── index.ts
├── tools/       # MCP tools implementation
│   ├── bondData.ts
│   ├── marketData.ts
│   └── searchBonds.ts
├── types/       # Type definitions
│   └── index.ts
├── utils/       # Utility functions
│   ├── errorHandler.ts
│   └── logger.ts
├── client.ts    # Example MCP client
├── index.ts     # Entry point
└── server.ts    # MCP server implementation
```

---

## Available scripts

- `pnpm run build` / `npm run build`: Build the project
- `pnpm start` / `npm start`: Start the server
- `pnpm run dev` / `npm run dev`: Start the server in development mode with auto-reload

---

## Contributing

Contributions are welcome! Please open an issue or submit a pull request on [GitHub](https://github.com/AtilioA/tesouro-direto-mcp).

---

## License

This project is licensed under the GNU Affero General Public License v3.0. See the [LICENSE](LICENSE) file for details.
