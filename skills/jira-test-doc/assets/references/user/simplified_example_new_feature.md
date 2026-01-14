# Simplified Example: New Feature

# Simplified Example: New Feature

## Input
```bash
/jira-test-doc MD-18000
```

## Jira Ticket
**Title:** Feature: Add bulk import for vendor SKUs

**Description:**
Allow users to import multiple vendor SKUs at once using an Excel file template. This will save time when onboarding new vendors with many products.

## Commits Found
```
f1a2b3c MD-18000 Add bulk import UI and file upload
d4e5f6g MD-18000 Implement validation and import logic
h7i8j9k MD-18000 Add import history tracking
```

## Generated Output
```
【What Changed】
Added a bulk import feature that lets users upload Excel files to add multiple vendor SKUs at once. The system validates the data before importing, shows progress during the import, and provides detailed error reports for any issues. Users can also view their import history to track past uploads and see what went wrong if there were errors.

【Affected Functions】
Vendor SKU page (new Bulk Import button), Import History page (new), Vendor Item Details page (shows import source).

【Test Suggestions】
- Test importing a valid Excel file with 10 SKUs - all should import successfully
- Test importing a file with errors (duplicates, missing fields) - valid rows should import, errors should be reported
- Test the Import History page shows all past imports with details and error logs
- Test the progress indicator works when importing 50+ SKUs
- Test uploading a file with wrong column format - should show clear error message
- Test that imported SKUs show correct data in the list

(From commits: f1a2b3c, d4e5f6g, h7i8j9k)
```