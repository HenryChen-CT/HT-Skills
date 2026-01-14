# Example: Bug Fix Documentation

# Example 1: Bug Fix

## Input
```bash
/jira-test-doc MD-17127
```

## Jira Ticket
**Title:** Bug: Deleting allergen doesn't update recipe allergen list

**Description:**
When a user deletes an allergen from the system, recipes that contained that allergen still show it in their allergen list. This causes confusion and incorrect allergen information.

**Acceptance Criteria:**
- Deleting an allergen should update all recipes using it
- System should prevent deletion of allergens in use
- User should see which recipes use the allergen

## Commits Found
```
a1b2c3d MD-17127 Fix allergen deletion to update recipes
e4f5g6h MD-17127 Add validation for allergen usage
```

## Generated Documentation
```markdown
h1. Test Documentation for MD-17127

h2. What I Changed
* Fixed the bug where deleting an allergen didn't update recipes containing that allergen
* Added validation to prevent deleting allergens that are still used in active recipes
* Updated the system to show which recipes use each allergen

h2. Affected Functions
* *Allergen Management Page*: Now shows warning when trying to delete allergens in use
* *Recipe Detail Page*: Allergen list updates immediately when allergens are deleted
* *Recipe Search*: Can still filter by allergens correctly after deletions

h2. Test Suggestions

h3. Test Scenario 1: Delete Unused Allergen
*Steps to test:*
# Go to Allergen Management page
# Create a test allergen that is not used in any recipe
# Click "Delete" button on that allergen
# Confirm deletion

*Expected Result:* Allergen is deleted successfully and removed from the list

h3. Test Scenario 2: Try to Delete Allergen in Use
*Steps to test:*
# Go to Allergen Management page
# Find an allergen used in active recipes (e.g., "Milk")
# Click "Delete" button
# Observe the warning message

*Expected Result:* System shows error: "Cannot delete allergen - used by X recipes" with a list of affected recipes

h3. Test Scenario 3: Verify Recipe Updates After Allergen Deletion
*Steps to test:*
# Create a test recipe with a test allergen
# Note the recipe's allergen list
# Delete the test allergen (if validation allows)
# Refresh the recipe page
# Check the allergen list

*Expected Result:* The deleted allergen is removed from the recipe's allergen list

---
_Generated from commits: a1b2c3d, e4f5g6h_
```