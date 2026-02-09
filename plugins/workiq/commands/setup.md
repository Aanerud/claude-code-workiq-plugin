---
description: Set up Microsoft Work IQ for first-time use with Claude Code
argument-hint: [tenant-id]
---

# Work IQ Setup Guide

Walk the user through setting up Microsoft Work IQ for use with Claude Code.

## Instructions

Guide the user through each prerequisite step:

### 1. Check Node.js

Run `node --version` to verify Node.js is installed. If not, direct the user to install it from https://nodejs.org (v18+ recommended).

### 2. Accept the EULA

Use the Work IQ MCP tool `accept_eula` with the EULA URL `https://github.com/microsoft/work-iq-mcp`. This must be accepted before any queries will work.

### 3. Microsoft 365 Requirements

Inform the user they need:
- A Microsoft 365 subscription with a Copilot license
- Their tenant administrator must have granted consent for Work IQ in Microsoft Entra

### 4. Test the Connection

Use the Work IQ MCP tool `ask_work_iq` with a simple test query like "What meetings do I have today?" to verify everything works.

If the MCP tools are not available (server not running), suggest the user restart Claude Code so the MCP server initializes, then try again.

### 5. Tenant Configuration (Optional)

If the user provided a tenant ID via $ARGUMENTS, note that tenant-specific configuration can be set via the CLI:

```
npx -y @microsoft/workiq ask -q "test" -t <tenant-id>
```

## Troubleshooting

### Authentication Errors
- Ensure the user is signed in to a Microsoft account with a Copilot license
- Tenant administrator must grant consent for Work IQ
- Reference: https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/workiq-overview

### MCP Server Not Responding
- Restart Claude Code — the MCP server starts at session launch
- Check that Node.js is installed and `npx` has internet access
- Try running `npx -y @microsoft/workiq mcp` manually to see error output

### No Results Returned
- Work IQ respects existing Microsoft 365 permissions
- The user can only access data they already have permission to view
- Try broader queries first to verify connectivity

### Slow Responses
- Queries typically take 5-15 seconds — this is the round-trip to Microsoft's services and is expected

## Resources

- GitHub: https://github.com/microsoft/work-iq-mcp
- Microsoft Docs: https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/workiq-overview
- Issues: https://github.com/microsoft/work-iq-mcp/issues
