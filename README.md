# EconDash plugin

[![EconDash MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/org.econdash/econdash/badges/score.svg)](https://glama.ai/mcp/connectors/org.econdash/econdash)

Public statistics for 290+ countries and regions, inside your AI assistant. EconDash has 750+ indicators in ten categories:

- macroeconomics: GDP, inflation, debt, trade;
- financial markets: interest rates, money supply, stock indices;
- labor: unemployment, employment structure;
- demographics: population, fertility, migration;
- real estate: house prices, construction spending;
- commodities and energy: oil, copper, electricity;
- transport and logistics: container ports, air passengers, railways;
- healthcare: life expectancy, health spending;
- education: school enrollment, literacy;
- technology and internet: internet use, mobile and broadband subscriptions.

The data comes from the World Bank, IMF, FRED, Eurostat, ECB, OECD, WHO and other public sources. Every figure arrives with its source, licence and a link to the chart on [econdash.org](https://econdash.org).

The plugin connects your assistant to the EconDash MCP server at `https://mcp.econdash.org/mcp`. It is read-only and free: the server never changes data and never takes payments. The server is listed in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=org.econdash) as `org.econdash/econdash`.

## What it can do

Ask questions in plain language, for example:

- "What is the latest GDP per capita of Germany according to EconDash?"
- "Compare unemployment in Spain and Germany in 2015, with sources."
- "How has the Brent oil price moved over the last ten years?"
- "Life expectancy at birth in Japan, South Korea and Italy."
- "Which EconDash indicators cover house prices?"
- "What is the source and licence of the EconDash CO2 emissions per capita data?"

The assistant gets these tools from the server:

| Tool | What it returns |
| --- | --- |
| `search_indicators` | Indicators matching a keyword, with slug, name, unit and frequency |
| `get_indicator_series` | Recent values of one indicator for one country or region |
| `get_full_series` | The whole history of a series (needs an EconDash sign-in, see below) |
| `compare_countries` | One indicator for up to 20 countries or regions |
| `get_indicator_details` | Description, unit, source, licence and coverage of an indicator |
| `list_countries` | Countries and regions as ISO 3166-1 alpha-3 codes |

## Install

### Claude Code

```
/plugin marketplace add econdash/econdash-plugin
/plugin install econdash@econdash
```

### Grok Build

```
grok plugin install https://github.com/econdash/econdash-plugin
```

### Gemini CLI

```
gemini extensions install https://github.com/econdash/econdash-plugin
```

### Other assistants

ChatGPT, Claude apps, grok.com, Cursor, VS Code and other MCP clients can connect to the server URL directly. Step-by-step instructions are in the [MCP documentation](https://econdash.org/docs/mcp).

## What data it sends

The plugin contains only configuration and text. It runs no code on your computer and reads no local files or environment variables.

When the assistant calls a tool, the EconDash server receives the tool name and its arguments: an indicator name, country codes, years or search words. It never receives your conversation, your files or your account with the AI platform. The server log stores no IP addresses. Details are in the [Privacy Policy](https://econdash.org/docs/privacy-policy).

## Signing in

Search, recent values, comparisons and indicator details work without an account. Only `get_full_series` asks you to sign in to EconDash; without it, the tool answers with a message and the assistant can use `get_indicator_series` instead.

- **Claude Code:** run `/mcp`, pick `plugin:econdash:econdash` and choose **Authenticate** (Claude Code may label it **Re-authenticate**).
- **Gemini CLI:** run `/mcp auth econdash`.
- **Claude (claude.ai, Desktop, mobile):** Claude offers to connect your account the first time the assistant calls `get_full_series`.

A page on econdash.org opens, you sign in and click **Allow**, and the assistant receives a read-only token. It never sees your password and cannot change your account or make payments.

If Claude Code lists EconDash as "needs authentication" and shows no EconDash tools (the server caused this after an anonymous `get_full_series` call until October 2026), sign in as above or run `claude mcp logout plugin:econdash:econdash`. The free tools come back in the next session.

## Limits

The server is shared, so it has rate limits. Clients that connect directly, such as Claude Code, Grok Build and Gemini CLI, get 30 tool calls per minute and 500 per day per IP address. For bulk downloads use the [data API](https://econdash.org/docs/quick-start).

## Links

- [MCP documentation](https://econdash.org/docs/mcp)
- [Privacy Policy](https://econdash.org/docs/privacy-policy)
- [Terms of Service](https://econdash.org/docs/terms-of-service)
- [Data licences](https://econdash.org/data-license)
- Support: support@econdash.org

## License

The plugin files are released under the [MIT License](LICENSE). The data returned by the server is covered by the licences of its original sources, listed on the [Data licences](https://econdash.org/data-license) page.
