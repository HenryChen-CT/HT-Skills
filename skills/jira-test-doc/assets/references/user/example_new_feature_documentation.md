# Example: New Feature Documentation

# Example 2: New Feature

## Input
```bash
/jira-test-doc MD-18000
```

## Jira Ticket
**Title:** Feature: Add bulk import for vendor SKUs

**Description:**
Allow users to import multiple vendor SKUs at once using an Excel file template. This will save time when onboarding new vendors with many products.

**Acceptance Criteria:**
- User can upload Excel file with SKU data
- System validates data before importing
- User sees progress and error report
- Successfully imported SKUs appear in the list

## Commits Found
```
f1a2b3c MD-18000 Add bulk import UI and file upload
d4e5f6g MD-18000 Implement validation and import logic
h7i8j9k MD-18000 Add import history tracking
```

## Generated Documentation
```markdown
h1. Test Documentation for MD-18000

h2. What I Changed
* Added ability to import multiple vendor SKUs at once using Excel files
* Created validation to check for duplicate SKU codes and missing required fields
* Added progress indicator showing import status
* Created import history page to track past imports

h2. Affected Functions
* *Vendor SKU Page*: New "Bulk Import" button added in the header
* *Import History Page*: New page accessible from main menu showing past imports and errors
* *Vendor Item Details*: Shows import source and date for imported items

h2. Test Suggestions

h3. Test Scenario 1: Import Valid Excel File
*Steps to test:*
# Go to Vendor SKU page
# Click "Bulk Import" button
# Download the Excel template
# Fill in 10 valid SKU records with all required fields
# Upload the file
# Click "Import"
# Wait for completion

*Expected Result:* All 10 SKUs imported successfully, shown in the SKU list with correct data (vendor name, SKU code, price, etc.)

h3. Test Scenario 2: Import File with Errors
*Steps to test:*
# Prepare Excel file with mixed data:
  - 5 valid SKUs
  - 2 duplicate SKU codes
  - 3 rows missing required fields (e.g., price or vendor name)
# Upload and click import
# Wait for completion
# Check the error report

*Expected Result:* 5 SKUs imported successfully, 5 rejected with detailed error messages explaining what's wrong with each row

h3. Test Scenario 3: Check Import History
*Steps to test:*
# Perform an import (success or failure)
# Go to main menu and click "Import History"
# Find your import in the list
# Click to view details

*Expected Result:* Shows import date, username, file name, success count, failure count, and downloadable error log

h3. Test Scenario 4: Import Progress Indicator
*Steps to test:*
# Prepare Excel file with 50+ SKUs
# Start the import
# Observe the progress bar
# Try to navigate away and come back

*Expected Result:* Progress bar shows percentage complete, user can navigate away and status persists, completion shows summary

h3. Test Scenario 5: Excel Template Validation
*Steps to test:*
# Download Excel template
# Verify column headers match documentation
# Try uploading file with wrong columns
# Observe error message

*Expected Result:* Template has correct columns, uploading wrong format shows clear error about column mismatch

---
_Generated from commits: f1a2b3c, d4e5f6g, h7i8j9k_
```