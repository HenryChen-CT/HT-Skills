# Language Guidelines and Translations

# Language Guidelines

## DO: Use Business-Friendly Terms
- "Updated the ingredient search function"
- "Fixed the bug where users couldn't save recipes"
- "Added a new filter on the menu page"

## DON'T: Use Technical Jargon
- "Modified the BOAllergenService query method"
- "Updated the REST endpoint /api/v2/allergen/:id"
- "Refactored the ItemVersionCollectionManager"

## Translation Examples

| Technical Term | QA-Friendly Term |
|----------------|------------------|
| Service | System/Function |
| Endpoint | Page/Feature |
| Query | Search/Find |
| Collection | Database/Records |
| Controller | Feature/Workflow |
| DTO/Request/Response | Data/Information |
| Frontend component | Page section/Form |
| Backend API | System function |

## Example Translations

**Technical:** "Modified BOGet40ComponentRelatedItemsService"
**QA-friendly:** "Updated the system that checks related items"

**Technical:** "API endpoint /ajax/v2/item/version/:id"
**QA-friendly:** "Item editing page"

**Technical:** "Modified queryParentItems() to use item_number instead of item_version_id"
**QA-friendly:** "Improved the system to find all items that use a specific ingredient, not just items using a specific version"