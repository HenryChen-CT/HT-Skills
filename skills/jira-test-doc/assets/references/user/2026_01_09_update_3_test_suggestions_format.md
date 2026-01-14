# 2026-01-09 Update 3: Test Suggestions Format

# 2026-01-09 Update 3: Test Suggestions Format

## Change Made

### Test Suggestions Should NOT Include Expected Results

**CRITICAL RULE**: Test suggestions should ONLY describe the test scenario/action, NOT the expected result.

## Why This Change

- QA already knows the expected behavior from the "What Changed" section
- Test suggestions should just list WHAT to test
- Reduces redundancy and makes documentation cleaner
- Focuses on test actions rather than duplicating requirements

## Format Change

**Before (with expected results):**
```
【Test Suggestions】
# Edit a 41* item and modify quantity - should display warning dialog
# Click Confirm button - should close dialog and proceed with save
```

**After (scenario only):**
```
【Test Suggestions】
# Edit a 41* item and modify its 40* ingredient quantity, then click save
# Click the Confirm button in the warning dialog
```

## Updated Documentation Files

- ✅ Updated: simplified_output_format.md - Removed expected results from examples
- ✅ Updated: language_and_content_requirements.md - Added to checklist
- ✅ Updated: formatting_best_practices.md - Added to common mistakes
- ✅ Created: test_suggestions_format.md - Complete guide on test suggestions format

## Key Points

1. Describe the test action/scenario only
2. Use clear, specific language
3. Cover different test cases (positive, negative, edge cases)
4. Focus on WHAT to test, not WHAT should happen
5. Let QA determine pass/fail based on requirements in "What Changed"

## Examples

✅ **Good:**
- Edit a WSKU item and change the ingredient quantity
- Navigate to the item detail page and click save
- Verify the warning dialog shows related items
- Test with an item that has no fulfillment options

❌ **Bad:**
- Edit item and verify warning appears
- Click save and check if dialog shows
- Confirm dialog closes after clicking
