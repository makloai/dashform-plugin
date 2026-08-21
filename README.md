# Dashform agent plugins

Official [Dashform](https://getaiform.com) plugins for AI coding agents. Dashform is an AI-powered form builder — describe a form in plain language, publish it, and let AI score every reply.

## Claude Code

The Claude Code plugin lives in [`claude/`](./claude). It connects the Dashform MCP server (`https://getaiform.com/api/mcp`) and ships:

- **`dashform` skill** — teaches Claude the full Dashform tool surface: form lifecycle (create → edit → publish), lead scoring, reply triage, analytics, integrations (Slack, HubSpot, Airtable, Mailchimp, Zapier, webhooks), org branding, custom domains, and media.
- **`/dashform:new-form`** — guided create → refine → score → publish workflow for a new form.

### Install

```
/plugin marketplace add makloai/dashform-plugin
/plugin install dashform@makloai
```

Then run `/mcp`, select **dashform**, and sign in with your Dashform account — auth is OAuth in the browser, no API key needed. Marketplace discovery and agent-funnel booking tools work without signing in.

### Requirements

- A free [Dashform](https://getaiform.com) account for the authenticated tools.
- Claude Code with plugin support.

## Other agents

The Dashform MCP server is agent-agnostic. For Cursor, Windsurf, Zed, and Claude Desktop install snippets, see [getaiform.com/.well-known/mcp.json](https://getaiform.com/.well-known/mcp.json) or [getaiform.com/llms.txt](https://getaiform.com/llms.txt). Plugins for more agents may land in this repo as sibling directories.

## Development

```bash
claude --plugin-dir ./claude          # run Claude Code with the local plugin
claude plugin validate ./claude       # validate the plugin manifest
claude plugin validate .              # validate the marketplace manifest
```
