# Update 2026-01-09: Concise "What Changed" Section

## Critical Rule: Keep What Changed Section Concise

The "What Changed" section should focus ONLY on:
1. **Entry point** - Where does the change occur?
2. **Trigger scenario** - What action triggers the change?
3. **Core functionality** - What happens at a high level?

## What to AVOID in What Changed

❌ **Do NOT include:**
- Button names and positions (e.g., "Confirm button at bottom-right")
- Link behaviors (e.g., "clickable links that open in a new window")
- Detailed conditional logic (e.g., "if X has no Y AND Z has no W, dialog won't show")
- Step-by-step UI interactions
- Expected results or outcomes
- Detailed dialog/popup behaviors

## Good Example (Concise)

✅ **Correct - Simple and to the point:**
```
【What Changed】
Added a reminder dialog feature to the 41* WSKU item editing page. When users modify the quantity of a 40* ingredient and click Save, a warning dialog appears showing two categories of related items:
# Fulfillment options (88* items) for the current 41* item
# Parent items (70* items and menu items) of the 40* ingredient

{expand:Filtering Logic Details}
[Detailed filtering logic here...]
{expand}
```

## Bad Example (Too Detailed)

❌ **Wrong - Too much UI detail:**
```
【What Changed】
Added a smart reminder feature to the 41* WSKU item editing page. When users modify the quantity of a 40* ingredient and click save, the system displays a warning dialog to help review potentially affected related items.

The dialog shows two types of related items:
# Fulfillment options (88* items) for the current 41* item
# Parent items (70* items and menu items) of the 40* ingredient

All item numbers are displayed as clickable links that open in a new window. The dialog includes a Confirm button at the bottom-right corner. When users click the Confirm button, the dialog closes and returns to the item detail page.

If the current 41* item has no fulfillment options AND its 40* ingredient has no parent items, the reminder dialog will not be displayed.
```

## Why This Matters

- QA doesn't need UI implementation details in the summary
- Keep the overview high-level and scenario-focused
- Let the Test Suggestions section cover the detailed test cases
- Detailed filtering logic belongs in {expand} sections
- Focus on WHAT changed and WHERE it happens, not HOW the UI behaves

## Quick Checklist

Before finalizing "What Changed":
- [ ] Entry point clearly stated?
- [ ] Trigger scenario clearly stated?
- [ ] Core functionality briefly described?
- [ ] No button/link behavior details?
- [ ] No conditional logic details?
- [ ] Filtering logic in {expand} if complex?
- [ ] Length is concise (~2-4 sentences for main text)?
