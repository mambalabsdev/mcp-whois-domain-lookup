# WHOIS Domain Lookup MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-whois-domain-lookup)](https://www.npmjs.com/package/@mambalabsdev/mcp-whois-domain-lookup) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-whois-domain-lookup)](https://github.com/mambalabsdev/mcp-whois-domain-lookup/blob/main/LICENSE)

An MCP server for the Mamba Labs WHOIS Domain Lookup actor on Apify. Give it domains, website URLs, or email addresses. For each domain it returns one row: whether it is registered, the registrar, the creation, update, and expiry dates, the domain age and days until expiry, the status codes, the nameservers, DNSSEC, and the registrant organization and country where the registry publishes them.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

The actor asks each registry directly: its RDAP server from the official IANA list, a registry RDAP server the list does not carry yet for .io, .ac, .co, .us, .ch, and .li, and the registry's port 43 WHOIS server for the rest. No key and no third party lookup service. A domain the registry does not hold returns `registered` false. All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-whois-domain-lookup": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-whois-domain-lookup"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `lookup_domain_whois` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "How old are these 200 prospect domains, and which ones expire in the next 90 days?"
- "Who is the registrar for acme.io, and when was it registered?"
- "Which of these domains are not registered?"

## Tool

`lookup_domain_whois`. One tool. Example arguments:

```json
{
  "domains": ["stripe.com", "notion.io", "lemonde.fr"]
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and yes or no options are sent as strings.

| Input | Type | Description |
|---|---|---|
| `domains` | array | Domains, URLs, or email addresses, up to 5,000 |
| `domain` | string | One domain |
| `follow_registrar_rdap` | string | true (default) or false |
| `include_raw` | string | true or false (default) |
| `max_charge_usd` | string | Optional cost cap for the run |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `domain-lookup`, per domain the registry answered for | $0.0025 | $0.002375 | $0.00225 | $0.002125 |
| `apify-actor-start`, per run start | $0.0006 | $0.0006 | $0.0006 | $0.0006 |

Rows with no dates published, error rows, input that is not a domain, and repeats of a domain in the same run are free.

## Your keys

The actor needs no key and holds none. It reads the registries' public RDAP and WHOIS services. Mamba Labs pays the platform costs of the run.

## Full actor documentation

[apify.com/mambalabs/whois-domain-lookup](https://apify.com/mambalabs/whois-domain-lookup)

## License

MIT. See [LICENSE](LICENSE).
