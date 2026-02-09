---
name: workiq-capabilities
description: This skill should be used when the user mentions a person's name, asks "who is", "who owns", "who works on", "what team", references a project by name, needs to find documents or design docs, asks about meetings or emails, mentions "Teams channel", discusses organizational context, asks about code ownership, or needs to find the right person to contact about code. Provides guidance on using Microsoft Work IQ to query Microsoft 365 data.
version: 1.0.0
---

# Microsoft Work IQ Capabilities

Work IQ is a Microsoft MCP server that connects Claude Code to the user's Microsoft 365 Copilot data. It enables natural language queries against workplace information including people, emails, meetings, documents, and Teams messages.

## When to Use Work IQ

### People Lookup
- User encounters a person's name in code, git history, or documentation
- User asks who owns, maintains, or is responsible for a service or component
- User needs contact information for a colleague
- User asks about someone's role, team, or reporting structure

### Project Context
- User references a project name found in code or documentation
- User needs to understand project scope, stakeholders, or status
- User asks about cross-team initiatives related to the codebase

### Document Discovery
- User needs to find design documents, RFCs, or architecture docs
- User references a document mentioned in code comments
- User needs specifications or requirements documents

### Communication Context
- User asks about email threads related to a topic
- User needs to find Teams channel discussions about a feature
- User wants meeting notes or decisions from relevant meetings

### Calendar and Scheduling
- User asks about upcoming meetings related to a project
- User needs to know about code review or planning meetings

## Example Queries

| Scenario | Query |
|----------|-------|
| Code ownership | "Who is the lead developer on the payments service?" |
| Person lookup | "What team does jane.doe@company.com belong to?" |
| Related emails | "What emails were sent about the API migration last week?" |
| Meeting context | "What was discussed in the architecture review meeting?" |
| Documents | "Find design documents for the notification system" |
| Teams | "What has been discussed in the Backend Engineering channel about caching?" |

## How to Use

The WorkIQ MCP server is configured in this plugin and provides tools for natural language queries. Use the `/workiq:ask` command for direct queries, or let the org-knowledge agent handle lookups automatically during code exploration.

## Prerequisites

Work IQ requires:
- Node.js installed locally
- Microsoft 365 subscription with Copilot license
- EULA accepted (`workiq accept-eula`)
- Tenant admin consent granted

If Work IQ is not set up, direct the user to `/workiq:setup`.

## Important Notes

- Work IQ respects existing Microsoft 365 permissions; users can only access data they have permission to view
- Results may be limited based on the user's organizational role
- Work IQ is currently in public preview; features may change
- For issues: https://github.com/microsoft/work-iq-mcp/issues
