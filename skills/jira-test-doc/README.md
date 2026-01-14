# jira-test-doc - Quick Reference

Generate QA-friendly test documentation from Jira tickets and Git commits.

## Quick Start

```bash
jira-test-doc <TICKET_ID>
```

Example:
```bash
jira-test-doc MD-17127
```

## What You Get

Automatically generated test documentation in Jira format with:

- **【What Changed】** - User-friendly description with filtering logic
- **【Affected Functions】** - List of impacted features/pages
- **【Test Suggestions】** - Test scenarios to verify the changes

## Key Features

✅ **English only** - All documentation in English
✅ **Filtering logic** - Includes detailed filter conditions and data exclusions
✅ **Proper formatting** - Numbered lists (#), line breaks, {expand} for details
✅ **User-friendly** - Translates technical terms to business language
✅ **Auto-post** - Posts directly to Jira after confirmation

## Critical Rules

| What | How |
|------|-----|
| Lists | Use `#` (numbered), NOT `-` (bullets) |
| Language | English only |
| Test suggestions | Action only, NO expected results |
| Filtering logic | Must include in "What Changed" |
| Complex details | Use `{expand:title}...{expand}` |
| Line breaks | Add blank lines between sections |

## Output Template

```
【What Changed】
[1-2 sentence summary]

Main changes:
# Change 1
# Change 2

{expand:Filtering Logic Details}
[Detailed filtering conditions]
{expand}

【Affected Functions】
# Function/Page 1
# Function/Page 2

【Test Suggestions】
# Test scenario 1 (action only)
# Test scenario 2 (action only)

(From commits: hash1, hash2)
```

## Quality Checklist

Before posting, verify:

- [ ] ALL content in English
- [ ] Using `#` not `-` for lists
- [ ] Line breaks between sections
- [ ] Filtering logic included
- [ ] `{expand}` used for complex details
- [ ] Test suggestions = actions only (no "should do X")
- [ ] Technical terms translated

## Common Code Patterns to Look For

When analyzing code changes:

- **Filters**: `eq`, `ne`, `in`, `and`, `or`
- **Status**: `DORMANT`, `ACTIVE`, `INACTIVE`, `deleted`
- **Versions**: `effective`, `deleted`
- **Deduplication**: `Set`, `distinct`, duplicate removal
- **Scope**: Multiple queries, BOM/customization searches

## Examples

### ✅ Good Test Suggestion
```
# Edit a 41* item and modify its 40* ingredient quantity, then click save
# Click any item number link in the warning dialog
# Test with an item that has no fulfillment options
```

### ❌ Bad Test Suggestion
```
# Edit item and verify warning appears
# Click link and check it opens new window
# Test no options - should not show warning
```

## Documentation

Full documentation available in `assets/references/user/`:

- `cheat_sheet.md` - Quick reference table
- `quick_reference_guide.md` - Detailed workflow guide
- `language_and_content_requirements.md` - Critical requirements
- `formatting_best_practices.md` - Formatting rules and examples
- `test_suggestions_format.md` - Test suggestions guide

## Search Documentation

```bash
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "query"
```

Examples:
```bash
# Search for formatting tips
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "formatting"

# Search for filtering examples
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "filtering logic"

# Search for examples
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "example"
```

## Typical Workflow

1. Complete your development work
2. Commit changes with ticket ID in message
3. Run `jira-test-doc TICKET-ID`
4. Review generated documentation
5. Confirm to post to Jira
6. Done! QA can start testing

---

**Pro Tip**: Run this immediately after committing for best results - fresh context helps generate more accurate documentation!
