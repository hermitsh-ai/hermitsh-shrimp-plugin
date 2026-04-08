---
name: hermitsh-shrimp
description: >
  This skill should be used when the user mentions "tasks", "to-do", "todo",
  "to do list", "reminders", "things to do", "my list", "what's on my plate",
  "add to my tasks", "check off", "mark done", "what do I need to do",
  "shrimp", or any reference to managing, creating, completing, organizing,
  or reviewing personal tasks. Also triggers when the user asks to plan,
  break down a project, schedule something, or track progress on goals.
version: 1.0.0
---

# SHrimp Task Management

SHrimp is a task management app on the user's phone. This plugin gives you direct access to their task tree — you can read, create, update, complete, archive, move, and delete tasks in real-time. Changes appear on their phone instantly.

## First-Time Setup

Before using any task tools, check if the plugin is paired:

1. Call `shrimp_status` to check the connection
2. If not paired, tell the user:
   > "I need to connect to your SHrimp account first. Open SHrimp on your phone, go to **Settings → Agents → Pair New Agent**, and give me the 6-digit code."
3. Once they provide the code, call `shrimp_pair` with the code and `agentName: "Claude"`
4. After successful pairing, proceed with their request

Do not repeatedly check status once paired — it persists across conversations.

## When to Use SHrimp Tools

Use SHrimp tools proactively whenever the conversation involves the user's tasks:

- User says "add X to my tasks" → `shrimp_add_task`
- User asks "what do I have to do?" → `shrimp_get_tasks`
- User says "mark groceries as done" → search for it, then `shrimp_complete_task`
- User wants to reorganize → use `shrimp_move_task` or `shrimp_batch`
- User describes a project → break it down and use `shrimp_batch` to create multiple tasks at once
- User asks about a specific task → `shrimp_search`

## Task Tree Structure

Tasks in SHrimp are hierarchical — any task can have children (subtasks). The tree can be arbitrarily deep, but typically 2-3 levels works best:

```
[ ] Plan Japan trip [travel]
  [ ] Book flights
  [ ] Research hotels
    [ ] Check Shinjuku options
    [ ] Compare Kyoto ryokans
  [ ] Create itinerary
```

## Categories

SHrimp supports these categories: `home`, `work`, `errands`, `health`, `people`, `money`, `travel`, `projects`. Assign categories when creating tasks to help the user filter and organize.

## Best Practices

- **Read before writing.** Always fetch the current task tree before making changes so you have accurate IDs and understand the existing structure.
- **Use batch for multiple changes.** If creating 3+ tasks or making several updates, use `shrimp_batch` instead of individual calls — it's faster and atomic.
- **Preserve hierarchy.** When adding tasks related to an existing parent, nest them using `parentID` rather than creating flat root-level tasks.
- **Be specific with titles.** "Buy groceries" is better than "Shopping". Include actionable detail.
- **Don't over-organize.** If the user says "remind me to call Mom", just create a single task. Don't create a "Phone calls" parent with a subtask.
- **Confirm destructive actions.** Before deleting or archiving multiple tasks, tell the user what you're about to remove.

## Tool Reference

See `references/tools.md` for detailed documentation on each available tool.
