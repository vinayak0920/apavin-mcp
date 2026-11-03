# Apavin for Claude and ChatGPT

Your business email, WhatsApp and LinkedIn in Claude or ChatGPT: answer customers in your own voice, follow up with
quiet buyers, write LinkedIn posts, and run background agents on a schedule. Nothing reaches a customer or goes public
until you approve it in Apavin.

This repository is the plugin: the Apavin skills and the connector. Apavin runs the server at
`https://mcp.apavin.com/mcp` (Streamable HTTP, OAuth). You need an Apavin account; the Free plan needs no card.

## Install in Claude

1. Open **Customize**, then **Plugins**, then **Add**, then **Add marketplace**.
2. Choose **Add from a repository**, enter `vinayak0920/apavin-mcp`, and choose **Sync**.
3. Open **Apavin** and choose **Add**.
4. On the **Connectors** tab, choose **Connect**, sign in to Apavin and allow access.

In Claude Code: `/plugin marketplace add vinayak0920/apavin-mcp`, then `/plugin install apavin@apavin`.

## Install in ChatGPT

Add a custom connector (developer mode) with the server URL `https://mcp.apavin.com/mcp`, sign in to Apavin and allow
access. Then type `@Apavin` in a chat.

## Background agents

Set up agents in Apavin under **Settings, MCP, Background agents**, then ask Claude: "Put my Apavin agents on a
schedule." The `apavin-agents` skill creates one scheduled task per agent. Each run shows in Apavin's log, and
everything it writes waits in **Approvals**.

## What's here

- `skills/apavin/`: how to work the inbox, WhatsApp and LinkedIn with Apavin's tools.
- `skills/apavin-agents/`: running background agents and scheduling them.
- `.claude-plugin/` and `.mcp.json`: the plugin and marketplace in Claude's format.
- `plugin.json` and `mcp.json`: the same plugin in the agent-plugins format for ChatGPT.
- `server.json`: the MCP Registry entry.
