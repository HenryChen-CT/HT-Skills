# Jira API ADF Format Rules (Updated 2026-01-16)

## CRITICAL: Converting Rules to ADF Format

When posting comments via Jira REST API, you must use **ADF (Atlassian Document Format)**, not wiki markup.

### Rule: Numbered Lists

The rule "Use # for numbered lists" refers to the **visual output** in Jira. When using the API with ADF, you must convert "#" to proper `orderedList` structure.

❌ **Wrong - Using # as text:**
```json
{
  "type": "paragraph",
  "content": [{"type": "text", "text": "# Item one"}]
}
```

✅ **Correct - Using orderedList:**
```json
{
  "type": "orderedList",
  "content": [
    {
      "type": "listItem",
      "content": [
        {
          "type": "paragraph",
          "content": [{"type": "text", "text": "Item one"}]
        }
      ]
    },
    {
      "type": "listItem",
      "content": [
        {
          "type": "paragraph",
          "content": [{"type": "text", "text": "Item two"}]
        }
      ]
    }
  ]
}
```

### Rule: Section Titles with 【】

Use bold text for section titles:

```json
{
  "type": "paragraph",
  "content": [
    {
      "type": "text",
      "text": "【What Changed】",
      "marks": [{"type": "strong"}]
    }
  ]
}
```

### Rule: {expand} Sections

Use the `expand` node type:

```json
{
  "type": "expand",
  "attrs": {"title": "Technical Details"},
  "content": [
    {
      "type": "paragraph",
      "content": [{"type": "text", "text": "Details here..."}]
    }
  ]
}
```

### Rule: Code Blocks

Use `codeBlock` with language attribute:

```json
{
  "type": "codeBlock",
  "attrs": {"language": "java"},
  "content": [{"type": "text", "text": "code here"}]
}
```

---

## ADF Structure Quick Reference

| Wiki Markup | ADF Node Type |
|-------------|---------------|
| # item | `orderedList` > `listItem` |
| - item | `bulletList` > `listItem` |
| {expand:title}...{expand} | `expand` with `attrs.title` |
| {code:java}...{code} | `codeBlock` with `attrs.language` |
| *bold* | text with `marks: [{"type": "strong"}]` |

---

## Checklist Before Posting

- [ ] All "#" lists converted to `orderedList` structure
- [ ] Section titles use `strong` marks
- [ ] {expand} sections use `expand` node type
- [ ] Code blocks use `codeBlock` with language
