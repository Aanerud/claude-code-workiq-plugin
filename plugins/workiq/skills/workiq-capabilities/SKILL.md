---
name: workiq-capabilities
description: Use this skill proactively during coding workflows that involve people, teams, or organizational context. Triggers include git blame output with email addresses, PR reviews, code ownership questions, finding design docs referenced in code, understanding decisions behind code changes, encountering person names in comments or documentation, onboarding to unfamiliar repos, and any mention of "who is", "who owns", "who works on", "what team", meetings, emails, or Teams channels.
version: 2.0.0
---

# Microsoft Work IQ — Proactive Coding Integration

Work IQ connects Claude Code to the user's Microsoft 365 environment via MCP. It answers natural language queries about people, emails, meetings, documents, and Teams messages.

## When to Use Work IQ Proactively

### Git Blame & Git Log

When you run `git blame` or `git log` and see email addresses or author names:
- Look up who they are, their role, and what team they're on
- Useful when the user asks "who wrote this?" or "who should I talk to about this code?"

| Trigger | Query |
|---------|-------|
| See `johndoe@company.com` in git blame | "Who is johndoe@company.com? What team are they on?" |
| See unfamiliar author in git log | "What is the role of Jane Smith?" |
| Multiple authors on a file | "Who is the manager of johndoe@company.com?" to find the team lead |

### Pull Request Reviews

When reviewing or creating PRs:
- Look up the PR author's role and team for context
- Find related design docs or specs that informed the change
- Find meeting notes where the change was discussed or decided

| Trigger | Query |
|---------|-------|
| Reviewing a PR from an unfamiliar author | "Who is sarah@company.com and what team are they on?" |
| PR references a project or initiative | "Find design documents for Project Phoenix" |
| PR implements a decision you need context on | "What was discussed in the architecture review meeting about caching?" |

### Code Ownership & Contacting People

When the user needs to know who owns, maintains, or is responsible for code:
- Find service owners, tech leads, and team structures
- Find the right person to contact about a change or bug

| Trigger | Query |
|---------|-------|
| "Who owns this service?" | "Who is the lead developer on the auth-service?" |
| Need to escalate or get approval | "Who is the manager of the payments team?" |
| Looking for a subject matter expert | "Who is working on the database migration project?" |

### Decision Archaeology

When code comments, commit messages, or PRs reference decisions but don't explain them:
- Find the meeting notes, email threads, or design docs that explain *why*
- Useful for understanding legacy code or controversial changes

| Trigger | Query |
|---------|-------|
| Comment says "per arch review decision" | "What was decided in the architecture review about the API gateway?" |
| Commit message references a project | "Find emails about Project Atlas from last month" |
| Code has a workaround with no explanation | "What was discussed in the Backend Engineering channel about rate limiting?" |

### Onboarding & Unfamiliar Repos

When a user is new to a codebase and needs organizational context:
- Understand the team structure behind the code
- Find documentation and specs
- Identify who to ask questions

| Trigger | Query |
|---------|-------|
| User says "I'm new to this repo" | "Who is the lead developer on [service name]?" |
| README references a team or project | "What team owns the notification service?" |
| Need to find specs or architecture docs | "Find design documents for the user authentication system" |

### Documents & Specs

When code references documents, RFCs, or specs:
- Find them in SharePoint or OneDrive
- Summarize key points without the user leaving their editor

| Trigger | Query |
|---------|-------|
| Code comment says "see design doc" | "Find design documents for [feature name]" |
| Need API specs or requirements | "Find the specification document for the REST API v2" |
| Looking for test plans or runbooks | "Find documents about deployment runbook for payments" |

### Meetings & Calendar

When work involves scheduled events:
- Find upcoming meetings related to the code being worked on
- Get meeting transcripts and decisions

| Trigger | Query |
|---------|-------|
| User is preparing for a review | "What meetings do I have about the API migration?" |
| Need context from a past meeting | "Summarize the standup transcript from yesterday" |

### Email & Teams

When the user needs communication context:
- Find email threads about a topic
- Search Teams channel discussions

| Trigger | Query |
|---------|-------|
| Looking for context on a decision | "What emails were sent about the database schema change?" |
| Need to check team discussions | "What has been discussed in the Platform Engineering channel about caching?" |

## How to Query

Use the Work IQ MCP tools directly. The tool accepts a single natural language question — keep queries specific and include names, email addresses, or project names when available.

Good queries:
- "Who is johndoe@company.com? What is their role and team?"
- "Find design documents for the notification system"
- "What was decided in last week's architecture review?"

Avoid:
- Bulk queries (each takes 5-15 seconds)
- Overly vague queries like "tell me everything about the company"

## Prerequisites

Work IQ requires:
- Node.js installed locally
- Microsoft 365 subscription with Copilot license
- Tenant admin consent granted

If Work IQ is not set up, direct the user to `/workiq:setup`.

## Important Notes

- Work IQ respects existing Microsoft 365 permissions; users can only access data they have permission to view
- Queries take 5-15 seconds due to Microsoft backend round-trips
- Results are natural language, not structured data
- For issues: https://github.com/microsoft/work-iq-mcp/issues
