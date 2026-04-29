# Connectors

## How tool references work

Skill files in this plugin use `~~category` as a placeholder for whatever tool the user has connected in that category. For example, `~~knowledge base` resolves to Notion, Confluence, Guru, or any other knowledge-base MCP server the user has connected.

The plugin is **tool-agnostic** — it describes the workflow in terms of categories rather than specific products. The bundled `.mcp.json` pre-configures recommended MCP servers, but any server in the same category works.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
|----------|-------------|------------------|---------------|
| Knowledge base | `~~knowledge base` | Notion, Atlassian (Confluence) | Guru, Coda |
| Cloud storage | `~~cloud storage` | Box, Egnyte | Google Drive, Dropbox, SharePoint, Microsoft 365 |
| Design tool | `~~design tool` | Figma, Canva | Miro, Sketch, Adobe XD, Framer |

## When the skill uses each connector

- **`~~knowledge base`** — Searched at the start of a session for prior Ikigai work, personal development docs, role descriptions, or journals.
- **`~~cloud storage`** — Searched at the start of a session for personal bios, prior assessments, or reflection notes.
- **`~~design tool`** — Optional follow-up after the Ikigai framework is complete: persists the four-circle diagram as an editable, shareable board.

## What if no connectors are available?

The skill still works. It will ask the user directly for any prior context, render the framework inline (if the surface supports JSX/HTML rendering) or as a markdown summary, and offer a Word export for a portable copy.
