# Language and Content Requirements

# Language and Content Requirements

## CRITICAL REQUIREMENTS

### 1. Language Requirement
**ALL test documentation MUST be written in ENGLISH.**

- Never generate documentation in Chinese or other languages
- All sections (What Changed, Affected Functions, Test Suggestions) must be in English
- Commit references and technical terms should remain in English

### 2. What Changed Section - Include Filtering Logic

The "What Changed" section MUST include key filtering logic details when applicable:

**IMPORTANT: Keep It Concise**
- Focus on entry point and trigger scenario ONLY
- Do NOT describe detailed dialog behavior, UI elements, or expected results
- Avoid mentioning buttons, links, or specific UI interactions in the main description
- Keep the scenario description brief and to the point

**Required Elements:**
- Entry point: Where does the change occur? (e.g., "41* WSKU item editing page")
- Trigger scenario: What action triggers the change? (e.g., "modify quantity and click Save")
- Core functionality: What happens? (e.g., "a warning dialog appears showing related items")
- Describe WHAT filters are applied to data (put details in {expand} if lengthy)
- Explain WHY certain items are included/excluded
- Mention specific filtering criteria like:
  - Source type filters (e.g., Wonder-sourced)
  - Status filters (active, inactive, dormant, deleted)
  - Version filters (effective, deleted)
  - Deduplication logic
  - Search scope (BOM usages, customization usages, etc.)

**Example - Good (Concise):**
"Added a reminder dialog feature to the 41* WSKU item editing page. When users modify the quantity of a 40* ingredient and click Save, a warning dialog appears showing two categories of related items: (1) Fulfillment options (88* items) for the current 41* item; (2) Parent items (70* items and menu items) of the 40* ingredient."

**Example - Bad (Too Detailed):**
❌ "Added a reminder dialog to the item editing page. The dialog displays related items with clickable links that open in a new window. All item numbers are hyperlinks. The dialog includes a Confirm button at the bottom-right that returns users to the item detail page. If the current item has no fulfillment options AND its ingredient has no parent items, the dialog will not appear."

**What to Avoid in Main Description:**
- Button names and locations (e.g., "Confirm button at bottom-right")
- Link behavior (e.g., "clickable links that open in a new window")
- Conditional logic details (e.g., "if X has no Y AND Z has no W, dialog won't show")
- Step-by-step UI interactions

### 3. Technical Accuracy

When analyzing code changes, pay attention to:
- Filter conditions in queries (eq, ne, in, and, or)
- Status checks (DORMANT, ACTIVE, INACTIVE)
- Collection queries and their predicates
- Deduplication logic (Set usage, distinct operations)
- Search scope (multiple collection queries, union of results)

### 4. Formatting Requirements

**Use Numbered Lists:**
- Use # for numbered lists in Jira (NOT bullet points -)
- Apply to all sections: "What Changed" sub-items, "Affected Functions", "Test Suggestions"

**Proper Line Breaks:**
- Add blank lines between sections
- Add blank lines between list items for better readability
- Separate summary from detailed lists

**Use {expand} for Complex Details:**
When filtering logic or technical details are lengthy, use Jira's expand feature:
```
{expand:Filtering Logic Details}
[Detailed filtering logic here]
{expand}
```

**Format Structure:**
```
【Section Title】
[Brief summary paragraph]

[Optional: Sub-section intro]
# Item 1
# Item 2

{expand:Details}
[Complex details here]
{expand}
```

### Implementation Checklist

When generating test documentation:
1. ✅ Verify the entire document is in English
2. ✅ Analyze all filter conditions in the code
3. ✅ Include filtering logic in "What Changed"
4. ✅ Make filtering logic specific and detailed
5. ✅ Use numbered lists (#) for all list items
6. ✅ Add proper line breaks between sections
7. ✅ Put complex filtering details in {expand} if too long
8. ✅ Test suggestions: describe test scenarios only, NO expected results
9. ✅ Ensure test suggestions cover filter edge cases
