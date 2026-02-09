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

Run this command and confirm it succeeds:

```
npx -y @microsoft/workiq accept-eula
```

### 3. Microsoft 365 Requirements

Inform the user they need:
- A Microsoft 365 subscription with a Copilot license
- Their tenant administrator must have granted consent for Work IQ in Microsoft Entra

### 4. Test the Connection

Run a simple test query to verify everything works:

```
npx -y @microsoft/workiq ask -q "What meetings do I have today?"
```

### 5. Tenant Configuration (Optional)

If the user provided a tenant ID via $ARGUMENTS, test with:

```
npx -y @microsoft/workiq ask -q "test" -t <tenant-id>
```

## Troubleshooting

### Authentication Errors
- Ensure the user is signed in to a Microsoft account with a Copilot license
- Tenant administrator must grant consent for Work IQ
- Reference: https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/workiq-overview

### MCP Server Not Responding
- Try running `npx -y @microsoft/workiq mcp` manually to see error output
- Check for firewall or proxy issues blocking npx

### No Results Returned
- Work IQ respects existing Microsoft 365 permissions
- The user can only access data they already have permission to view
- Try broader queries first to verify connectivity

## Resources

- GitHub: https://github.com/microsoft/work-iq-mcp
- Microsoft Docs: https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/workiq-overview
- Issues: https://github.com/microsoft/work-iq-mcp/issues
