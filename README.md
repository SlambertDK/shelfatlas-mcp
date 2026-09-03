# ShelfAtlas MCP server

Danish grocery catalog and shelf data as MCP tools. Ask *"where is Pepsi Max
cheapest right now?"* and get live, structured answers: current offers across
every major Danish chain, nearest-store geo search, product name and EAN
lookup, and a purpose-built `find_cheapest_offers` tool. Community shelf-stock
signals are included where approved, with confirmation counts.

- **Endpoint:** `https://api.shelfatlas.com/api/v1/mcp` (Streamable HTTP)
- **Auth:** `Authorization: Bearer sa_live_<your-key>` — create a free key at
  <https://app.shelfatlas.com>
- **Docs:** <https://shelfatlas.com/docs> (tools, quotas, error codes)

## Tools

| Tool | What it answers |
|---|---|
| `search_products` | Resolve a product name to id + EAN before calling other tools |
| `get_product_by_ean` | Look up a product by EAN-13 barcode |
| `find_cheapest_offers` | "Where is this product cheapest right now?" — live offers, cheapest first, chain resolved |
| `search_catalog_offers` | Catalog offers with price and validity window (live-only by default; chain/EAN/product filters) |
| `get_stores` | Paginated store list, or nearest-first geo search |
| `list_chains` | All retail chains (id, slug, name) |

## Claude Desktop

Claude Desktop reaches remote servers through [`mcp-remote`](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "shelfatlas": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://api.shelfatlas.com/api/v1/mcp"],
      "env": {
        "MCP_REMOTE_HEADER_AUTHORIZATION": "Bearer sa_live_<your-key>"
      }
    }
  }
}
```

Clients with native Streamable HTTP support connect directly to the endpoint
with the `Authorization` header.

This repository only holds the registry manifest (`server.json`) and this
README; the server itself runs at shelfatlas.com.
