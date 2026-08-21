---
name: new-form
description: Create and publish a Dashform form from a plain-language description
---

Create a Dashform form from this description: $ARGUMENTS

Follow this workflow using the `dashform` MCP server:

1. If the description above is empty, ask the user what the form is for, who fills it in, and what a "good" respondent looks like.
2. Confirm the workspace: call `get_user_info`; if the user belongs to several organizations and the target is ambiguous, list them with `list_organizations` and ask which to use, then `switch_active_org` if needed.
3. Strengthen the description with `refine_prompt`, then create the form with `create_form`.
4. Review the generated questions with `get_form_questions` and show the user a concise summary. Apply their requested changes through `chat_form_editor`.
5. Offer lead scoring: run `suggest_scoring_criteria`, show the suggestions, and save the ones the user approves with `update_scoring_criteria`.
6. When the user is happy, publish with `publish_form` and reply with the published share URL plus one-line pointers to replies and integrations as next steps.

If any authenticated call fails with an auth error, tell the user to sign in and then continue: in Claude Code via `/mcp` → **dashform**; in Codex via `codex mcp login dashform`.
