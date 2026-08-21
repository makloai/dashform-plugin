---
name: dashform
description: Work with Dashform (getaiform.com), the AI form builder — create, edit, and publish forms and quizzes, triage replies and lead scoring, wire integrations (Slack, HubSpot, Airtable, Mailchimp, Zapier, webhooks), manage org branding and custom domains, or book through a merchant's agent funnel. Use whenever the user mentions Dashform, getaiform.com, or wants to build or operate an AI form, quiz, or lead-capture funnel through it.
---

# Dashform

Dashform is an AI-powered form builder. This plugin connects the `dashform` MCP server at `https://getaiform.com/api/mcp`; every capability below is an MCP tool on that server.

## Connection and auth

- Most tools require OAuth. If authenticated tool calls fail with an auth error, tell the user to run `/mcp`, select **dashform**, and complete the browser sign-in (OAuth with dynamic client registration — no API key needed).
- A small public subset works without auth: marketplace discovery (`list_categories`, `search_merchants`, `search_services`) and agent-funnel booking (`get_business_info`, `get_services`, `get_form_questions`, `check_fit`, `get_availability`, `book_appointment`).

## Active organization

Authenticated tools act on the connection's **active organization**, resolved from the OAuth token — never from tool input. Check identity with `get_user_info`, enumerate orgs with `list_organizations`, and change scope with `switch_active_org`. When results look like the wrong workspace, verify the active org first.

## Destructive actions

Destructive tools (deletes, batch deletes, revokes) require `confirm: true` in the tool input and fail without it. Get the user's explicit go-ahead before passing it.

## Form lifecycle

1. **Create** with `create_form` from a natural-language description. `refine_prompt` can strengthen a vague description first; `import_agent_profile` bootstraps a form from a business's public web presence.
2. **Inspect** with `list_forms`, `get_form`, and `get_form_questions`. Versions matter: `get_form_version` reads a draft revision, `get_published_form_version` reads what respondents actually see.
3. **Edit** with `update_form` for direct field changes, or `chat_form_editor` for conversational, multi-step editing of questions and logic — prefer `chat_form_editor` for anything beyond a simple property change.
4. **Publish** with `publish_form`. Publishing snapshots a version; later edits are drafts until published again.
5. **Delete** with `delete_form` (destructive — see above).

## Lead scoring and replies

- Scoring: `get_form_scoring_state` shows the current criteria; `suggest_scoring_criteria` drafts criteria with AI; `update_scoring_criteria` saves them; `rescore_form_replies` re-runs scoring over existing replies after criteria change.
- Replies: `list_replies` / `get_reply` to read, `get_replies_insights` for AI summaries, `list_organization_hot_lead_counts` for hot-lead overviews across forms. Triage with `mark_actioned` and `override_verdict` (correct a lead's AI verdict). `create_reply` submits a reply; `delete_reply` / `batch_delete_replies` are destructive.
- `analytics_chat` answers natural-language questions over form analytics — reach for it before assembling numbers by hand.

## Integrations

- CRUD: `list_integrations`, `get_integration`, `create_integration` (guided) or `create_integration_from_config`, `toggle_integration`, `delete_integration`.
- Provider pickers for configuration: `list_slack_channels`, `list_airtable_bases`, `list_hubspot_contact_properties`, `list_mailchimp_audiences`.
- Delivery debugging: `list_integration_events` shows delivery history; `replay_integration_event` re-sends a failed event.
- Zapier and raw webhooks: `list_zapier_hooks`, `toggle_zapier_hook`, `delete_zapier_hook`, `create_webhook_connection`.
- OAuth connections behind integrations: `list_connections`, `get_connection`, `delete_connection`, `revoke_connection`.

## Organization settings

- Branding: `get_org_branding` / `update_org_branding`; email sending: `get_org_email_config` / `update_org_email_config`.
- Custom domains: `list_custom_domains`, `add_custom_domain`, `verify_custom_domain` (after the user sets DNS), `set_custom_domain_default_form`, `remove_custom_domain`.
- BYOK AI keys (owner-only): `get_ai_provider_status`, `save_ai_provider_key`, `remove_ai_provider_key`.
- Billing: `get_quiz_credits_status`, `create_quiz_credits_checkout`, `reconnect_quota_precheck`.

## Media

`upload_blob` / `delete_blob` for form assets, `search_photos` / `search_videos` for licensed stock media to use in forms, and `transcribe` for audio.

## Conventions

- Form share URLs and the dashboard live on `getaiform.com` (or the org's verified custom domain). Give the user the published share URL after publishing.
- Tool results use an ok/err envelope; on `err`, read the message — common causes are missing auth, wrong active org, plan limits, or a missing `confirm` flag.
