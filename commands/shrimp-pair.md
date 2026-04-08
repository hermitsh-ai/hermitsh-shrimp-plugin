---
description: Connect to a SHrimp account
allowed-tools: ["mcp__shrimp__shrimp_pair", "mcp__shrimp__shrimp_status"]
---

Help the user pair this plugin with their SHrimp account.

First, call shrimp_status to check if already connected. If already paired, tell the user and ask if they want to re-pair.

If not paired, ask the user to:
1. Open SHrimp on their phone
2. Go to Settings → Agents → Pair New Agent
3. Share the 6-digit code that appears

Once they provide the code, call shrimp_pair with the code and agentName "Claude".

Report the result — on success, confirm what scopes were granted. On failure, explain the error and suggest they try generating a new code.
