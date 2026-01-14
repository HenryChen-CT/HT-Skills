# Simplified Example: Bug Fix

# Simplified Example: Bug Fix

## Input
```bash
/jira-test-doc MD-17127
```

## Jira Ticket
**Title:** Bug: Deleting allergen doesn't update recipe allergen list

**Description:**
When a user deletes an allergen from the system, recipes that contained that allergen still show it in their allergen list.

## Commits Found
```
a1b2c3d MD-17127 Fix allergen deletion to update recipes
e4f5g6h MD-17127 Add validation for allergen usage
```

## Generated Output
```
【What Changed】
Fixed a bug where deleting an allergen from the system didn't remove it from recipes that use it. The system now automatically updates all affected recipes and shows a warning if you try to delete an allergen that's still being used. You can also see which recipes use each allergen before deleting.

【Affected Functions】
Allergen Management page, Recipe Detail page allergen list, Recipe Search allergen filter.

【Test Suggestions】
- Test deleting an unused allergen - should be deleted successfully
- Test deleting an allergen used in recipes - should show error with list of recipes
- Test that recipe pages no longer show the deleted allergen after deletion
- Test that recipe search allergen filter works correctly after allergen deletion

(From commits: a1b2c3d, e4f5g6h)
```