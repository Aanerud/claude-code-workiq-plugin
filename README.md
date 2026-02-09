# WorkIQ Plugin for Claude Code

> Connect Claude Code to your Microsoft 365 environment via Work IQ

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This plugin integrates [Microsoft Work IQ](https://github.com/microsoft/work-iq-mcp) into Claude Code, enabling you to query your Microsoft 365 data — people, emails, meetings, documents, and Teams messages — directly while coding.

**Use case**: When working in a codebase and you encounter a person's name in git blame, need to find the owner of a service, want to look up meeting notes about an architecture decision, or need to find related documents — WorkIQ brings your organizational context directly into your coding workflow.

## How It Works

This plugin is a **Claude Code integration layer** on top of Microsoft's [Work IQ MCP server](https://github.com/microsoft/work-iq-mcp). Work IQ itself is the engine that authenticates with Microsoft 365 and queries your organizational data. This plugin adds:

- **Slash commands** (`/workiq:ask`, `/workiq:setup`) for direct interaction
- **An agent** (`org-knowledge`) that Claude automatically uses when you mention people, teams, or projects
- **A skill** (`workiq-capabilities`) that teaches Claude when Work IQ is relevant to your task
- **MCP server configuration** so Claude Code starts Work IQ automatically

When the plugin is installed, Claude Code launches the Work IQ MCP server as a background process at session start. Queries go through the MCP protocol directly — there's no shell fallback or manual `npx` calls needed.

## Performance

Queries to Work IQ typically take **5–15 seconds** to return. This is expected — each query authenticates with Microsoft Entra, hits the Microsoft 365 Copilot backend, and processes a natural language response. This is not a limitation of the plugin; it's the round-trip to Microsoft's services.

## Prerequisites

- [Node.js](https://nodejs.org) (v18+)
- Microsoft 365 subscription with Copilot license
- Tenant admin consent (see [setup guide](https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/workiq-overview))

## Installation

### Step 1: Add the marketplace

```
/plugin marketplace add Aanerud/claude-code-workiq-plugin
```

### Step 2: Install the plugin

```
/plugin install workiq@aanerud-plugins
```

### Step 3: Restart Claude Code

The MCP server starts at session launch. Restart Claude Code after installing so the Work IQ server initializes.

### Step 4: First-time setup

Run `/workiq:setup` in Claude Code to verify your configuration and complete authentication.

## What's Included

### MCP Server

The plugin configures Claude Code to start the Work IQ MCP server automatically via `npx -y @microsoft/workiq mcp`. This uses `npx` so no global npm install is required — it downloads and runs the latest version on-the-fly. If you already have `@microsoft/workiq` installed globally, `npx` will use your local copy.

### Slash Commands

| Command | Description |
|---------|-------------|
| `/workiq:ask <question>` | Query your M365 environment directly |
| `/workiq:setup` | First-time setup and troubleshooting guide |

### Agent: org-knowledge

Claude automatically dispatches to this agent when you encounter person names, project references, or need organizational context while coding. No manual invocation needed.

### Skill: workiq-capabilities

Provides Claude with knowledge about what Work IQ can do, so it proactively suggests using it when relevant to your task.

## Example Queries

```
/workiq:ask Who is my manager?
/workiq:ask Who is the lead developer on the payments service?
/workiq:ask What emails did I get from Sarah about the API migration?
/workiq:ask What meetings do I have tomorrow?
/workiq:ask Find documents about the Q4 architecture review
/workiq:ask Summarize today's messages in the Platform Engineering channel
```

## Security & Privacy

- Work IQ respects your existing Microsoft 365 permissions
- You can only access data you already have permission to view
- Authentication is handled by Microsoft Entra (Azure AD)
- No credentials are stored by this plugin
- The MCP server runs locally on your machine

## Troubleshooting

Run `/workiq:setup` in Claude Code for interactive troubleshooting, or:

- **Empty responses**: Make sure you've restarted Claude Code after installing the plugin so the MCP server is running
- **Auth errors**: Verify your tenant admin has granted consent for Work IQ
- **No results**: Check your M365 permissions and try broader queries
- **Server not starting**: Verify Node.js is installed and `npx` has internet access
- **Slow responses**: This is expected — see [Performance](#performance) above
- **Issues**: https://github.com/microsoft/work-iq-mcp/issues

## Contributing

Contributions welcome! Please open an issue or pull request.

## License

MIT — see [LICENSE](LICENSE)

## Acknowledgments

- [Microsoft Work IQ](https://github.com/microsoft/work-iq-mcp) for the MCP server
- [Claude Code](https://claude.ai/code) plugin system
