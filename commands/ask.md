---
description: Query your Microsoft 365 environment via Work IQ (people, emails, meetings, documents, Teams)
argument-hint: <question about people, emails, meetings, documents, or Teams>
---

# Work IQ Query

Query the user's Microsoft 365 environment using Work IQ to answer their question.

## Arguments

The user's question: $ARGUMENTS

## Instructions

1. Take the user's question from $ARGUMENTS
2. Use the WorkIQ MCP server tools to answer the question
3. If the MCP tools are unavailable, fall back to the Bash tool:
   ```
   npx -y @microsoft/workiq ask -q "<question>"
   ```
4. Present the results clearly and concisely:
   - For people queries: include name, role, team, and contact info when available
   - For document queries: include document names and relevant snippets
   - For email/Teams queries: summarize key points and participants
   - For meeting queries: include time, attendees, and agenda/notes

## Error Handling

If the query fails with an authentication or setup error:
- Inform the user that Work IQ requires initial setup
- Suggest running `/workiq:setup` for a guided walkthrough
- Do not retry failed authentication attempts

If no results are returned:
- Suggest rephrasing or broadening the question
- Note that Work IQ only returns data the user has permission to access

## Example Usage

```
/workiq:ask Who is the lead developer on the payments service?
/workiq:ask What emails did I get from Sarah about the API migration?
/workiq:ask What meetings do I have tomorrow?
/workiq:ask Find documents about the Q4 architecture review
/workiq:ask Summarize today's messages in the Platform Engineering channel
```
