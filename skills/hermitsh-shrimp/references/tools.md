# SHrimp Tool Reference

## Connection Tools

### shrimp_pair
Pair this plugin with a SHrimp account. Only needed once — the connection persists.

- `code` (required): 6-digit pairing code from the SHrimp app
- `agentName` (optional, default "Claude"): Display name shown in the user's app

### shrimp_status
Check whether the plugin is connected. Returns email and connection state.

## Read Tools

### shrimp_get_tasks
Fetch the full task tree. Supports filters:

- `category`: Filter to one category (home, work, errands, health, people, money, travel, projects)
- `completed`: "true" or "false" to filter by completion
- `archived`: "true" to include archived tasks (excluded by default)
- `subtree`: Task ID to get only that branch
- `flat`: "true" for a flat list with parentID instead of nested children

Returns: version number, last-updated timestamp, and the task tree.

### shrimp_search
Search tasks by keyword (case-insensitive substring match on titles and notes).

- `q` (required): Search query
- `limit` (optional, default 20, max 50): Number of results

Returns: Matching tasks with breadcrumb paths showing hierarchy.

## Write Tools

### shrimp_add_task
Create a single task.

- `title` (required): Task title
- `notes`: Additional details
- `parentID`: UUID of parent task (omit for root level)
- `dueDate`: ISO 8601 date
- `category`: One of the 8 categories
- `insertBefore`: UUID of sibling to insert before (for ordering)

### shrimp_update_task
Modify an existing task. Only include fields you want to change.

- `taskID` (required): UUID of the task
- `title`, `notes`, `dueDate`, `category`: New values

### shrimp_complete_task
Toggle completion. Marks incomplete tasks as done, and done tasks as incomplete.

- `taskID` (required): UUID of the task

### shrimp_archive_task
Hide a task and its children from the active view. Not a deletion — can be restored.

- `taskID` (required): UUID of the task

### shrimp_restore_task
Bring an archived task back to the active list.

- `taskID` (required): UUID of the task

### shrimp_move_task
Reparent or reorder a task.

- `taskID` (required): UUID of the task to move
- `parentID`: New parent UUID (omit to move to root)
- `insertBefore`: UUID of sibling to insert before

### shrimp_delete_task
Permanently remove a task and all children. The user can undo on their phone, but the agent cannot.

- `taskID` (required): UUID of the task

### shrimp_batch
Execute up to 50 operations atomically. Each op has a `type` and relevant fields:

```json
{
  "ops": [
    { "type": "create", "title": "New task", "parentID": "..." },
    { "type": "complete", "taskID": "..." },
    { "type": "update", "taskID": "...", "notes": "Updated notes" },
    { "type": "move", "taskID": "...", "parentID": "..." },
    { "type": "delete", "taskID": "..." }
  ]
}
```

Types: create, update, complete, archive, restore, move, delete.

## AI Pipeline Tools

### shrimp_prompt
Send a plain-English instruction to the user's phone AI. The phone processes it through the user's configured AI provider. Good for complex restructuring that's easier to describe than to execute step by step.

- `prompt` (required): Natural language instruction
- Rate limited: 10 per hour

### shrimp_prompt_status
Check progress of a previously sent prompt.

- `promptID` (required): ID returned by shrimp_prompt
