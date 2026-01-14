# Simplified Output Format

# Simplified Output Format

The skill now generates a concise, paragraph-based summary instead of complex Jira formatting:

## Format Structure

```
【What Changed】
[Brief summary in 1-2 sentences]

Main changes:
# [Change 1 with summary]
# [Change 2 with summary]

[If filtering logic is complex, use {expand} to hide details]

【Affected Functions】
# [Function/Page 1]
# [Function/Page 2]

【Test Suggestions】
# [Test case 1: Brief description of test scenario]
# [Test case 2: Brief description of test scenario]
# [Test case 3: Brief description of test scenario]

(From commits: hash1, hash2, hash3)
```

## Key Principles

1. **ENGLISH ONLY** - ALL documentation MUST be written in English
2. **Keep What Changed concise** - Focus on entry point and trigger scenario ONLY; avoid detailed UI behavior descriptions
3. **Use numbered lists (#)** - Use # for numbered lists in Jira, NOT bullet points (-)
4. **Proper line breaks** - Add line breaks between sections and list items for readability
5. **Use {expand} for details** - If filtering logic or details are lengthy, put them in {expand:title}...{expand}
6. **Concise summary first** - Start with high-level summary, then list specific changes
7. **Include filtering logic** - In "What Changed", describe filter conditions, excluded items, search scope (in {expand} if lengthy)
8. **Keep language translation rules** - Technical terms → user-friendly language
9. **Target length** - ~150-250 words for main content (details can go in expand)

## Example Output (WITH Proper Formatting)

```
【What Changed】
Added a reminder dialog feature to the 41* WSKU item editing page. When users modify the quantity of a 40* ingredient and click Save, a warning dialog appears showing two categories of related items:
# Fulfillment options (88* items) for the current 41* item
# Parent items (70* items and menu items) of the 40* ingredient

{expand:Filtering Logic Details}
Fulfillment Options Query:
- Filtered to include only Wonder-sourced fulfillment options
- Only effective versions are included
- Deleted items are excluded

Parent Items Query:
- Searched through both BOM usages and customization usages
- Only effective versions are included
- Deleted and dormant items are excluded
- Duplicate item numbers are removed
{expand}

【Affected Functions】
# Item editing page (41* WSKU items)
# Ingredient quantity modification
# Save validation and warning functionality

【Test Suggestions】
# Edit a 41* item and modify its 40* ingredient quantity, then click save
# Edit a 41* item without modifying the quantity, then click save
# Verify the warning dialog displays the correct fulfillment options (88* items) list, excluding dormant items
# Verify the warning dialog displays the correct parent items list, including all 70*/menu items linked through both BOM and customization usages, excluding dormant items
# Click any item number link in the warning dialog
# Click the Confirm button in the warning dialog

(From commits: e024184579, e4130f8002)
```