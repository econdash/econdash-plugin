# Security

## Reporting a vulnerability

Email **support@econdash.org** with "Security" in the subject. Please do not open a public issue for a security problem.

Include what you found, how to reproduce it and what an attacker could do with it. We usually reply within two business days, investigate every report and tell you what we changed. There is no bug bounty.

## Scope

- This repository: the plugin manifests, skills, `.mcp.json` and `GEMINI.md`.
- The MCP server at `https://mcp.econdash.org/mcp`, including its OAuth sign-in.
- The website and API at `https://econdash.org`.

The plugin contains no executable code. It connects the assistant to the MCP server above and sends it only the tool arguments (indicator, country codes, years, search words). See the [Privacy Policy](https://econdash.org/docs/privacy-policy) for what the server logs.

## Supported versions

Fixes go into the latest release. Older versions are not patched; update to the latest release.
