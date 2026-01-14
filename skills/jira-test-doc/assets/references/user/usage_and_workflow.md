# Usage and Workflow

# Usage

## Basic Usage
```bash
/jira-test-doc MD-17127
```

This will:
1. Fetch the Jira ticket MD-17127
2. Find branch containing "MD-17127" (case-insensitive)
3. Find all commits from that branch
4. Analyze code changes
5. Generate test documentation
6. Post documentation to Jira as a comment

## Interactive Mode
If you don't provide a ticket number:
```bash
/jira-test-doc
```
The skill will ask you for the ticket number interactively.

## Workflow Steps

### Step 1: Read Jira Ticket Context
- Uses Jira MCP tool (mcp__jira__jira_get)
- Fetches ticket description, summary, and acceptance criteria
- Extracts business requirements and user stories

### Step 2: Find Related Commits
**IMPORTANT: Commits must be from branches containing the ticket keyword.**

Process:
1. Find branch with ticket keyword: `git branch -a | grep -i "<ticket-number>"`
2. Get commits from that branch: `git log <branch-name> --oneline --no-merges | head -20`
3. Get detailed changes: `git show <commit-hash> --stat`
4. Read key code changes: `git show <commit-hash>` (full diff)

This ensures only commits from the ticket's development branch are analyzed, avoiding unrelated changes from other branches.

### Step 3: Analyze Code Changes
- Identifies modified files (backend, frontend, database)
- Maps technical changes to business functionality
- Determines user-facing impacts

### Step 4: Generate Documentation
Creates structured documentation with:
- Plain language description of changes
- List of affected features and pages
- Concrete test scenarios with step-by-step instructions

### Step 5: Post to Jira (Optional)
- Asks user confirmation
- Posts as comment using Jira MCP tool (mcp__jira__jira_post)
- Includes all generated documentation