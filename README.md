# Photonesto MCP server for ChatGPT and Claude

**Connect Photonesto to ChatGPT, Claude and other AI agents through Cotlet.dev.** Your agent works in your signed-in Cloud Browser to review photo orders, prepare galleries and read client selections. Review client-visible changes before confirming them.

## What you can ask

> List my photo orders that still need delivery.

> Prepare a proofing gallery for my next family session for my approval.

> Read the photos my client starred for their wedding album.

> Review my product price lists.

> Export my client list for me to review.

## Connect your agent

Sign up at https://cotlet.dev/signup?app=photonesto, enable Photonesto and sign in to your account in the Cotlet.dev Cloud Browser.

### ChatGPT

Add `https://cotlet.dev/mcp/v1/connect` as a connector and sign in to Cotlet.dev.

### Claude

Add `https://cotlet.dev/mcp/v1/connect` as a custom connector and sign in to Cotlet.dev.

### Claude Code

Get an API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` into your project and set `COTLET_API_KEY` in your environment.

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Photonesto tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"photonesto":{"command":"uvx","args":["photonesto-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t photonesto-mcp .
docker run -i --rm -e COTLET_API_KEY photonesto-mcp
```

Tools: `photonesto_guide`, `photonesto_status`, `photonesto_open`, `photonesto_read`, `photonesto_click`, `photonesto_type`, `photonesto_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install photonesto-mcp        # or run it once: uvx photonesto-mcp connect
photonesto-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 photonesto_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 photonesto_agent.py status    # is Photonesto ready in your Cotlet.dev account
python3 photonesto_agent.py guide     # Photonesto screens and sign-in link
python3 photonesto_agent.py read      # open Photonesto, read the page, close the browser
python3 photonesto_agent.py tools     # list Cotlet.dev tools
python3 photonesto_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Photonesto users

**Does Photonesto have a public API?**

The Cotlet.dev integration page reports no public Photonesto API or developer documentation, and no official MCP server or ChatGPT or Claude connector was found, checked 17 November 2026.

**How do I connect Photonesto to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=photonesto, enable Photonesto and sign in at https://galleries.photonesto.com/ in your Cotlet.dev Cloud Browser. Add https://cotlet.dev/mcp/v1/connect as a connector in ChatGPT and sign in to Cotlet.dev.

**Can I connect Photonesto to Claude?**

Yes. Add https://cotlet.dev/mcp/v1/connect as a custom connector in Claude and sign in to Cotlet.dev.

**Can my agent email all my clients?**

The integration page lists no tool for sending email. It can export the client list for you to review.

**Is this an official Photonesto MCP server?**

No. Cotlet.dev is independent and is not affiliated with Photonesto.

## Source

[Photonesto on Cotlet.dev](https://cotlet.dev/integrations/photonesto-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=photonesto)

---

More: https://cotlet.dev/integrations/photonesto-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=photonesto

Start free: https://cotlet.dev/signup?app=photonesto&utm_source=github&utm_medium=readme&utm_campaign=photonesto
