# Connectors

## How tool references work

Skill files in this plugin use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~knowledge base` resolves to Notion, Confluence, Guru, or any other knowledge-base MCP the user has connected.

This plugin is **tool-agnostic** — it describes workflows in terms of categories rather than specific products. The bundled `.mcp.json` pre-configures specific MCP servers, but any MCP server in that category works.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
| --- | --- | --- | --- |
| Knowledge base | `~~knowledge base` | Notion, Atlassian (Confluence) | Guru, Coda |
| Cloud storage | `~~cloud storage` | Box, Egnyte | Google Drive, Dropbox, SharePoint, Microsoft 365 |
| Design tool | `~~design tool` | Figma, Canva | Miro, Sketch, Adobe XD |
| Project tracker | `~~project tracker` | Asana, Linear, Atlassian (Jira) | monday, ClickUp |

## When each connector is used

- **`~~knowledge base`** — Searched at the start of every skill in the kit for prior Ikigai work, executive summary drafts, mission/values docs, and OKR history. Helps the kit pick up where you left off if you've worked through any of these before. Also a recommended export destination for finalized mission/values docs and OKR sets.
- **`~~cloud storage`** — Searched for founder bios, prior assessments, reflection notes, market research, pitch decks. Useful both for picking up prior context and for storing exports.
- **`~~design tool`** — Optional follow-up step in `personal-ikigai`: persists the four-circle Ikigai framework as an editable, shareable board.
- **`~~project tracker`** — Used by `okr-workflow-pre-pmf` to publish OKRs to a project management tool with owner/period/priority properties, and to surface project context (tasks completed, milestones hit, blockers) when grading previous OKRs.

## What if I don't have any of these connected?

The plugin works without any connector. It'll fall back to asking you directly for context, and to text/markdown output. Connecting any of the above just makes the kit richer — pulling in your existing work and producing better-integrated outputs.
