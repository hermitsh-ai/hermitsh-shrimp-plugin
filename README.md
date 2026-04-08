# SHrimp — by hermitsh

Manage your tasks from Claude. Create, organize, search, and complete tasks with natural language. Works instantly with zero setup — tasks stored locally. Optionally pair with the SHrimp iOS app for phone sync, email-to-task pipeline, and push notifications.

## What You Can Do

- Ask Claude about your tasks: "What's on my plate today?"
- Add tasks naturally: "Remind me to call the dentist tomorrow"
- Break down projects: "Help me plan my apartment move"
- Reorganize: "Move all the work tasks under a new 'Q2 Goals' parent"
- Complete in bulk: "Mark everything in the groceries list as done"

## Setup

1. Install this plugin in Claude
2. Open SHrimp on your phone → Settings → Agents → Pair New Agent
3. Tell Claude the 6-digit code (or use `/shrimp-pair`)
4. Done — Claude can now manage your tasks

## Available Tools

| Tool | What It Does |
|------|-------------|
| `shrimp_pair` | Connect to your SHrimp account |
| `shrimp_status` | Check connection status |
| `shrimp_get_tasks` | Read your task tree |
| `shrimp_search` | Find tasks by keyword |
| `shrimp_add_task` | Create a new task |
| `shrimp_update_task` | Edit a task's details |
| `shrimp_complete_task` | Mark a task done (or undone) |
| `shrimp_archive_task` | Archive a task |
| `shrimp_restore_task` | Restore an archived task |
| `shrimp_move_task` | Move/reorder a task |
| `shrimp_delete_task` | Permanently remove a task |
| `shrimp_batch` | Execute multiple operations at once |
| `shrimp_prompt` | Send instructions to your phone's AI |
| `shrimp_prompt_status` | Check prompt progress |

## Commands

| Command | Description |
|---------|-------------|
| `/shrimp-pair` | Connect or reconnect to a SHrimp account |

## Requirements

- Node.js 18+
- SHrimp iOS app with an account
