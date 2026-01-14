# Formatting Best Practices

# Formatting Best Practices

## Why Good Formatting Matters

Good formatting makes test documentation:
- Easy to scan and read
- Professional looking
- Easy for QA to follow
- Clear in structure and priority

## Formatting Rules

### 1. Use Numbered Lists (#) Not Bullets (-)

**ALWAYS use:**
```
# Item 1
# Item 2
# Item 3
```

**NEVER use:**
```
- Item 1
- Item 2
- Item 3
```

### 2. Add Line Breaks for Readability

**Good (with line breaks):**
```
【What Changed】
Summary paragraph here.

Main changes:
# Change 1
# Change 2

Additional context here.
```

**Bad (no line breaks):**
```
【What Changed】
Summary paragraph here.
Main changes:
# Change 1
# Change 2
Additional context here.
```

### 3. Use {expand} for Complex Details

When filtering logic or technical details are long, use expand:

```
【What Changed】
Brief summary of the change in 1-2 sentences.

The system applies the following filters:
# Filter type 1 (brief description)
# Filter type 2 (brief description)

{expand:Detailed Filtering Logic}
Filter Type 1:
- Condition 1: Include only items where status = ACTIVE
- Condition 2: Exclude items where deleted = true
- Condition 3: Only effective versions

Filter Type 2:
- Searches through BOM usages table
- Searches through customization usages table
- Deduplicates by item_number
- Excludes DORMANT status
{expand}
```

### 4. Structure Template

Use this structure for all test documentation:

```
【What Changed】
[1-2 sentence summary]

[Optional: Context or breakdown]
# Main change 1
# Main change 2

[Optional: Additional context]

{expand:Technical Details}
[Detailed filtering logic, queries, etc.]
{expand}

【Affected Functions】
# Function/Page 1
# Function/Page 2
# Function/Page 3

【Test Suggestions】
# Test case 1: [test scenario description]
# Test case 2: [test scenario description]
# Test case 3: [test scenario description]
# Test case 4: [test scenario description]

(From commits: hash1, hash2, hash3)
```

## Common Mistakes to Avoid

❌ **Using bullet points instead of numbered lists**
✅ Use # for all lists

❌ **No line breaks between sections**
✅ Add blank lines for readability

❌ **All details in main text, making it too long**
✅ Use {expand} for complex details

❌ **Long paragraphs without structure**
✅ Break into summary + numbered list

❌ **Mixing Chinese and English**
✅ ALL content must be in English

❌ **Including expected results in test suggestions**
✅ Describe test scenarios only, NO expected results
