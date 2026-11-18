# RootMention MCP server

A public, remote [Model Context Protocol](https://modelcontextprotocol.io) server from [RootMention](https://rootmention.com), an SEO subscription service that gets brands found on Google and recommended by ChatGPT, Claude and Gemini.

It lets an AI assistant run a quick SEO audit of a website, estimate whether an SEO budget can pay for itself, and look up RootMention's plan.

- **Endpoint:** `https://rootmention.com/mcp`
- **Transport:** Streamable HTTP
- **Auth:** none
- **Cost:** free

## Tools

| Tool | What it does |
|---|---|
| `run_seo_audit` | Audits a public homepage and up to two discovered product or collection pages: indexing directives, page titles, H1 headings, meta descriptions, canonical tags, image alt text, internal links and HTTPS. Returns the findings inline. Requires the user to confirm they own or are authorized to audit the site. Respects robots.txt and is rate limited. |
| `calculate_seo_break_even` | Estimates the extra orders and visits needed to cover a monthly SEO spend, from order value, contribution margin and conversion rate. A scenario calculation, not a forecast. |
| `get_services` | Returns RootMention's plan (one flat $299 a month), what it includes and excludes, and links to pricing, contact and the free audit. |

All tools are read-only. Audited page content is treated as untrusted data.

## Connect

### Claude Desktop / Claude.ai

Add a custom connector with the URL `https://rootmention.com/mcp`.

Or, for clients that use a JSON config with `mcp-remote`:

```json
{
  "mcpServers": {
    "rootmention": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://rootmention.com/mcp"]
    }
  }
}
```

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "rootmention": {
      "url": "https://rootmention.com/mcp"
    }
  }
}
```

### VS Code

```json
{
  "servers": {
    "rootmention": {
      "type": "http",
      "url": "https://rootmention.com/mcp"
    }
  }
}
```

### Cline

Open Cline's MCP Servers panel, choose **Configure MCP Servers**, and add:

```json
{
  "mcpServers": {
    "rootmention": {
      "type": "streamableHttp",
      "url": "https://rootmention.com/mcp"
    }
  }
}
```

No API key is needed.

### Claude Code

```bash
claude mcp add --transport http rootmention https://rootmention.com/mcp
```

## Example prompts

- "Run an SEO audit on example.com. I own the site."
- "My average order is $60 at a 35% margin and a 2% conversion rate. How many extra orders would cover $299 a month of SEO?"
- "What does RootMention's SEO plan include?"

## Limits

- Audits check returned HTML on at most three pages. They don't run JavaScript or measure rankings, traffic, backlinks or AI visibility.
- One audit at a time, with an hourly limit per IP address. Each audit takes up to 35 seconds.

## About RootMention

RootMention is a founder-run SEO subscription for product brands, ecommerce stores, SaaS, gyms and local businesses. Each month it publishes AI-search content, fixes on-page and schema issues, and tracks how ChatGPT, Claude and Gemini describe your brand. One flat $299 a month, cancel anytime.

- Website: https://rootmention.com
- Free audit: https://rootmention.com/free-audit
- Contact: hello@rootmention.com

## License

The documentation in this repository is MIT licensed. The server itself is hosted by RootMention.
