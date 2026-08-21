# Dashform agent plugin

Official [Dashform](https://getaiform.com) plugin for Claude Code and OpenAI Codex. Dashform is an AI-powered form builder — describe a form in plain language, publish it, and let AI score every reply.

The plugin connects the Dashform MCP server (`https://getaiform.com/api/mcp`) and ships:

- **`dashform` skill** — teaches Claude the full Dashform tool surface: form lifecycle (create → edit → publish), lead scoring, reply triage, analytics, integrations (Slack, HubSpot, Airtable, Mailchimp, Zapier, webhooks), org branding, custom domains, and media.
- **`/dashform:new-form`** — guided create → refine → score → publish workflow for a new form.

## Install

### Claude Code

```
/plugin marketplace add makloai/dashform-plugin
/plugin install dashform@dashform-plugin
```

Then run `/mcp`, select **dashform**, and sign in with your Dashform account.

### Codex

```bash
codex plugin marketplace add makloai/dashform-plugin
codex plugin add dashform
codex mcp login dashform
```

Then start a new Codex session and invoke the skill with `@dashform`.

Auth is OAuth in the browser for both agents — no API key needed. Marketplace discovery and agent-funnel booking tools work without signing in.

## Requirements

- A free [Dashform](https://getaiform.com) account for the authenticated tools.
- Claude Code with plugin support.

## Other agents

The Dashform MCP server is agent-agnostic. For Cursor, Windsurf, Zed, and Claude Desktop install snippets, see [getaiform.com/.well-known/mcp.json](https://getaiform.com/.well-known/mcp.json) or [getaiform.com/llms.txt](https://getaiform.com/llms.txt).

## Development

```bash
claude --plugin-dir .          # run Claude Code with the local plugin
claude plugin validate .       # validate the plugin and marketplace manifests
```

## License

[MIT](./LICENSE)
