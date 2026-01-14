# 2026-01-09 Update 2: Formatting Requirements

# 2026-01-09 Update 2: Formatting Requirements

## Changes Made

### 1. Added Numbered List Requirement
- **CRITICAL**: Use # for numbered lists in Jira, NOT bullet points (-)
- Apply to ALL sections: What Changed, Affected Functions, Test Suggestions
- This makes documentation more professional and easier to follow

### 2. Added Line Break Requirements
- Add blank lines between sections
- Add blank lines between list items for better readability
- Separate summary from detailed lists
- Makes documentation easier to scan

### 3. Added {expand} Usage for Complex Details
- Use Jira's {expand:title}...{expand} syntax for lengthy details
- Put complex filtering logic in expand sections
- Keeps main content concise while providing full details
- Example: {expand:Filtering Logic Details}...{expand}

### 4. Updated Documentation Files
- ✅ Updated: simplified_output_format.md
  - Updated format structure to show # usage
  - Updated key principles to include formatting rules
  - Updated example to demonstrate proper formatting with {expand}
- ✅ Updated: language_and_content_requirements.md
  - Added section 4: Formatting Requirements
  - Added formatting to implementation checklist
- ✅ Created: formatting_best_practices.md
  - Complete guide on formatting rules
  - Examples of good vs bad formatting
  - Common mistakes to avoid
- ✅ Updated: simplified_workflow_guide.md
  - Updated output format rules to include formatting

## Why These Changes

These requirements emerged from:
1. Need for better readability in Jira comments
2. Professional presentation of test documentation
3. Ability to hide complex details while keeping summary clear
4. Consistency across all test documentation

## Impact

Future test documentation will:
- Use numbered lists (#) instead of bullets (-)
- Have proper line breaks for readability
- Use {expand} for complex filtering logic
- Be more scannable and professional

## Format Comparison

**Before (no formatting):**
```
【Test Suggestions】
- Test case 1
- Test case 2
- Test case 3
```

**After (with formatting):**
```
【Test Suggestions】
# Test case 1: [scenario] - [expected result]

# Test case 2: [scenario] - [expected result]

# Test case 3: [scenario] - [expected result]
```

**Complex Details (with expand):**
```
【What Changed】
Summary paragraph.

Main changes:
# Change 1
# Change 2

{expand:Filtering Logic Details}
Detailed filtering conditions here...
{expand}
```
