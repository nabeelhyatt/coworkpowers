# Connectors

CoworkPowers uses `~~` category placeholders throughout its agent prompts. These map to whatever MCP tools you have connected — the plugin is tool-agnostic.

## Supported Categories

| Category | Placeholder | Example MCPs |
|----------|------------|--------------|
| Email | `~~email` | Gmail (Google Workspace MCP), Microsoft 365 |
| Calendar | `~~calendar` | Google Calendar, Microsoft 365 |
| Meeting Notes | `~~meeting notes` | Granola |
| CRM | `~~crm` | Affinity, Salesforce, HubSpot |
| Company Intel | `~~company intel` | Harmonic, Clearbit |
| Chat | `~~chat` | Slack, Microsoft Teams, Discord |
| Knowledge Base | `~~knowledge base` | Notion, Confluence, Guru, Coda |
| Project Tracker | `~~project tracker` | Asana, Linear, Jira, monday.com, ClickUp |

## How It Works

The `/coworkpowers:workflow-research` skill runs a Phase 0 that discovers what MCP tools are available in your environment. It passes this info to all agents so they can use the right tools for the task.

No MCP connections are required. The plugin works with web search and local files alone — MCPs just make it better.
