# Quick Start Guide

# Quick Start Guide

## What is jira-test-doc?
A Claude Code skill that automatically generates QA-friendly test documentation from Jira tickets and Git commits.

## Installation
Already installed at: `/Users/sunrise/.claude/skills/jira-test-doc`

## Quick Usage
```bash
# Generate test documentation for a ticket
/jira-test-doc MD-17127

# This will:
# 1. Read the Jira ticket
# 2. Find related commits
# 3. Analyze code changes
# 4. Generate test scenarios
# 5. Ask if you want to post to Jira
```

## Output Example
The skill generates Jira-formatted documentation IN ENGLISH with three sections:
1. **What I Changed** - Plain language description of changes WITH filtering logic details
2. **Affected Functions** - Which features/pages are impacted
3. **Test Suggestions** - Concrete test scenarios with steps

## Key Features
- Generates ALL documentation in English
- Includes detailed filtering logic in "What Changed" section
- Translates technical jargon into business-friendly language
- Analyzes both Jira context and Git commits
- Creates actionable test scenarios
- Posts directly to Jira as comments
- Handles errors gracefully

## Common Commands
```bash
# Search the skill documentation
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "workflow"

# Add custom knowledge
skill-creator add-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" --title "My Pattern" --content "..."
```

## Need Help?
- Search for "troubleshooting" for common issues
- Search for "example" to see sample outputs
- Search for "best practices" for tips