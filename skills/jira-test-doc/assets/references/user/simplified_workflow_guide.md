# Simplified Workflow Guide

# Simplified Workflow Guide

## Usage
```bash
/jira-test-doc <JIRA_TICKET_ID>
```

Example:
```bash
/jira-test-doc MD-17127
```

## Workflow Steps

1. **Read Jira Ticket**: Fetch and analyze the ticket context
2. **Find Commits**: Search git history for commits mentioning the ticket ID
3. **Analyze Changes**: Review code changes in the commits, paying attention to:
   - Filter conditions in queries (eq, ne, in, and, or)
   - Status checks (DORMANT, ACTIVE, INACTIVE, deleted)
   - Collection queries and their predicates
   - Deduplication logic (Set usage, distinct operations)
   - Search scope (multiple collection queries, union of results)
4. **Generate Summary**: Create a simple paragraph-based summary IN ENGLISH with:
   - 【What Changed】: 2-3 sentences in user-friendly language, INCLUDING key filtering logic
   - 【Affected Functions】: 1-2 sentences listing impacted features
   - 【Test Suggestions】: Bullet points with test scenarios
5. **Ask User**: Confirm if they want to post the summary to Jira

## Output Format Rules

- **ENGLISH ONLY** - ALL documentation MUST be written in English
- **Use numbered lists (#)** - Use # for all lists, NOT bullet points (-)
- **Proper line breaks** - Add blank lines between sections and lists
- **Use {expand} for details** - Put complex filtering logic in {expand:title}...{expand}
- **Concise summary first** - Start with 1-2 sentence summary, then detailed list
- **Include filtering logic** - describe what filters are applied and why
- **User-friendly language** - translate technical terms
- **Commit references** - show at the end

## Language Translation Rules

Translate technical terms to user-friendly language:
- "ItemVersion" → "item" or "product"
- "MongoDB collection" → "database"
- "REST API endpoint" → "system interface"
- "Frontend component" → "page" or "screen"
- "Boolean flag" → "switch" or "option"

## When to Use

- Before moving a ticket to testing
- When QA needs context about changes
- To document what was changed for team reference