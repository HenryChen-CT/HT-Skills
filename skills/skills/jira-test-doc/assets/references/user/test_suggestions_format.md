# Test Suggestions Format

# Test Suggestions Format

## CRITICAL RULE

**Test Suggestions should ONLY describe the test scenario, NOT the expected result.**

## Correct Format

✅ **Good - Only scenario:**
```
【Test Suggestions】
# Edit a 41* item and modify its 40* ingredient quantity, then click save
# Edit a 41* item without modifying the quantity, then click save
# Verify the warning dialog displays the correct fulfillment options list
# Click the Confirm button in the warning dialog
```

## Incorrect Format

❌ **Bad - Includes expected result:**
```
【Test Suggestions】
# Edit a 41* item and modify quantity - should display warning dialog
# Edit without modifying quantity - should not show warning
# Click Confirm button - should close dialog and save
```

## Why?

QA knows what the expected behavior should be based on the "What Changed" section. Test suggestions should just list the actions to test, not duplicate the expected outcomes.

## Examples

### Good Examples:
- Edit a WSKU item and change the ingredient quantity
- Navigate to the item detail page and click the save button
- Verify the warning dialog shows the correct related items
- Test with an item that has no fulfillment options
- Test with dormant items in the database

### Bad Examples (Don't do this):
- Edit item and verify warning appears ❌
- Click save and check if dialog shows ❌
- Confirm dialog closes after clicking ❌
- Test that dormant items are excluded ❌

## Key Points

1. Describe the test action/scenario only
2. Use clear, specific language
3. Cover different test cases (positive, negative, edge cases)
4. Focus on WHAT to test, not WHAT should happen
5. Let QA determine pass/fail based on the requirements in "What Changed"
