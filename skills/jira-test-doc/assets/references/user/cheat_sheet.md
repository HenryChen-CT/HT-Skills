# Cheat Sheet

# jira-test-doc Cheat Sheet

## Command
```
/jira-test-doc <TICKET_ID>
```

## Output Format

```
【What Changed】
[Summary in 1-2 sentences]

Main changes:
# Change 1
# Change 2

{expand:Filtering Logic Details}
[Complex filtering details here]
{expand}

【Affected Functions】
# Function 1
# Function 2

【Test Suggestions】
# Test scenario 1 (action only, NO result)
# Test scenario 2
# Test scenario 3

(From commits: hash1, hash2)
```

## Critical Rules

| Rule | ✅ Do | ❌ Don't |
|------|------|----------|
| Language | English only | Chinese/other languages |
| Lists | Use # (numbered) | Use - (bullets) |
| Line breaks | Add blank lines | Compact text |
| Filtering | Include in "What Changed" | Omit details |
| Expand | Use {expand} for complex details | Put all in main text |
| Test suggestions | Describe action only | Include expected result |
| Technical terms | User-friendly language | Technical jargon |

## Quick Checklist

Copy this when reviewing your documentation:

```
□ ALL English
□ Using # not -
□ Line breaks added
□ Filtering logic included
□ {expand} used for complex details
□ Test suggestions = actions only
□ Technical terms translated
```

## Filter Analysis Keywords

When analyzing code, look for:
- `eq`, `ne`, `in`, `and`, `or` (filter conditions)
- `DORMANT`, `ACTIVE`, `INACTIVE`, `deleted` (status filters)
- `effective`, `deleted` (version filters)
- `Set`, `distinct` (deduplication)
- Multiple queries = describe search scope

## Example Test Suggestions

✅ **Good:**
```
# Edit a 41* item and change ingredient quantity, then click save
# Click the Confirm button in the warning dialog
# Test with an item that has no fulfillment options
```

❌ **Bad:**
```
# Edit item - should show warning
# Click Confirm - dialog should close
# Test no options - should not show warning
```

## Common Translations

| Technical | User-Friendly |
|-----------|---------------|
| Service | System/Function |
| Endpoint | Page/Feature |
| Collection | Database |
| DTO/Request | Data |
| Frontend component | Page section |
| Backend API | System function |
| ItemVersion | Item |
| Boolean flag | Switch/Option |

## Workflow

1. Commit your changes
2. Run `/jira-test-doc TICKET-ID`
3. Review generated documentation
4. Confirm to post to Jira
5. Done!

---

**Pro Tip:** Run this right after committing - fresh context = better documentation!
