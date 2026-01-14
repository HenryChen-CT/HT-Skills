# Output Format

# Output Format

The skill generates Jira-formatted markdown:

```markdown
h1. Test Documentation for MD-17127

h2. What I Changed
* Fixed the bug where deleting an ingredient didn't update recipes that use it
* Updated the system to recalculate nutrition facts for all affected recipes
* Added validation to prevent deleting ingredients still in use

h2. Affected Functions
* *Recipe Editor*: Now shows warning when trying to use deleted ingredients
* *Nutrition Calculator*: Automatically recalculates when ingredients change
* *Ingredient Management Page*: Shows which recipes use each ingredient

h2. Test Suggestions

h3. Test Scenario 1: Delete Ingredient Not in Use
*Steps to test:*
# Go to Ingredient Management page
# Find an ingredient that is not used in any recipe
# Click "Delete" button
# Confirm deletion

*Expected Result:* Ingredient is deleted successfully without errors

h3. Test Scenario 2: Try to Delete Ingredient in Use
*Steps to test:*
# Go to Ingredient Management page
# Find an ingredient used in active recipes
# Click "Delete" button
# Observe the warning message

*Expected Result:* System prevents deletion and shows list of recipes using this ingredient

---
_Generated from commits: a1b2c3d, e4f5g6h_
```