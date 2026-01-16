# Conciseness and Title Rules (Updated 2026-01-15)

## CRITICAL RULES

### Rule 1: NO Title Header
**DO NOT add a title like "Test Documentation for MD-XXXXX" at the beginning of the comment.**

❌ **Bad - Has title:**
```
Test Documentation for MD-17248

【What Changed】
...
```

✅ **Good - No title, starts directly with content:**
```
【What Changed】
...
```

**Why:** The Jira comment is already associated with the ticket. Adding a redundant title wastes space and makes it harder to scan.

---

### Rule 2: Keep ENTIRE Comment Concise
**Target length: 300-500 words TOTAL for the entire comment (excluding {expand} sections)**

The comment is too long if:
- Test Suggestions section has more than 15-20 items
- What Changed section is more than 3-4 paragraphs
- Total word count exceeds 500 words (before expand sections)

---

## How to Keep It Concise

### 1. Group Related Test Cases
Instead of listing every single test case separately, group similar ones:

❌ **Bad - Too detailed (20+ separate items):**
```
【Test Suggestions】
# Test THOUSANDTHS rounding with Density AVG=1.0528, SD=0.002
# Test HUNDREDTHS rounding with Water Activity AVG=0.8544, SD=0.005
# Test TENTHS rounding with pH AVG=4.55, SD=0.25
# Test TENTHS rounding with Cut Dimension Length AVG=2.55, SD=0.35
# Test ONES rounding with Weight AVG=19.25, SD=1.55
# Test ONES rounding with Color L AVG=19.25, SD=1.55
# Test ONES rounding with Moisture AVG=25.49, SD=2.1
# Test TENS rounding with Texture Peak Force AVG=181.75, SD=40.35
# Test HUNDREDS rounding with Viscosity AVG=2670.65, SD=100.15
# Test HUNDREDS rounding with Turbidity AVG=1180.03, SD=200.11
... (10+ more items)
```

✅ **Good - Grouped and concise (5-6 items):**
```
【Test Suggestions】
# Test basic range calculation with Weight AVG=20, SD=2
# Test all 6 rounding rules (THOUSANDTHS for Density, HUNDREDTHS for Water Activity, TENTHS for pH, ONES for Weight/Color/Moisture, TENS for Texture, HUNDREDS for Viscosity)
# Test all 6 constraint types (NON_NEGATIVE, COLOR_RANGE, PH_RANGE, TURBIDITY_RANGE, WATER_ACTIVITY_RANGE, PERCENTAGE_RANGE)
# Test UI validation with constraint violations (pH=15, Water Activity SD too large, Color A=-105)
# Verify spec export format change and backward compatibility
# Test backfill controller and change history tracking
```

### 2. Use High-Level Categories
Focus on categories of tests, not individual test cases:

❌ **Bad - Lists every single edge case:**
```
# Enter Weight AVG=20.0 with SD=0.0
# Test very small values with Density AVG=0.0001, SD=0.00001
# Test very large values with Viscosity AVG=50000.0, SD=5000.0
# Test rounding edge case with Weight AVG=20.5, SD=0.25
```

✅ **Good - Groups edge cases:**
```
# Test edge cases (zero SD, very small/large values, rounding .5 values)
```

### 3. Move Details to {expand}
Put specific test data, technical details, or lengthy descriptions in {expand} sections:

✅ **Good - Uses expand:**
```
【Test Suggestions】
# Test all rounding rules (6 precision levels)
# Test all constraint types (6 categories)

{expand:Detailed Test Data Examples}
Rounding Rules:
- THOUSANDTHS: Density AVG=1.0528, SD=0.002 → Range: 1.049 to 1.057
- HUNDREDTHS: Water Activity AVG=0.8544, SD=0.005 → Range: 0.84 to 0.86
- TENTHS: pH AVG=4.55, SD=0.25 → Range: 4.1 to 5.1
- ONES: Weight AVG=19.25, SD=1.55 → Range: 16 to 22
- TENS: Texture AVG=181.75, SD=40.35 → Range: 100 to 260
- HUNDREDS: Viscosity AVG=2670.65, SD=100.15 → Range: 2500 to 2900

Constraint Types:
- NON_NEGATIVE: Weight AVG=3.0, SD=2.0 → min capped at 0
- COLOR_RANGE: Color A AVG=-95, SD=4 → min=-100 (capped), max=-87
- PH_RANGE: pH AVG=1.0, SD=0.7 → min=0 (capped), max=2.4
- TURBIDITY_RANGE: AVG=40, SD=10 → enforces min 100 rule
- WATER_ACTIVITY_RANGE: AVG=0.98, SD=0.02 → max=1.0 (capped)
- PERCENTAGE_RANGE: Moisture AVG=98, SD=1.5 → max=100 (capped)
{expand}
```

### 4. Prioritize P0 Tests Only
In the main list, only include P0 (critical) test cases. P1 and P2 tests can go in {expand} or be omitted.

---

## Target Structure

```
【What Changed】
[1-2 sentence summary - 50 words max]

Main changes:
# [3-5 key changes]

{expand:Technical Details}
[Put implementation details here]
{expand}

【Affected Functions】
# [3-5 affected areas]

【Test Suggestions】
# [5-10 high-level test categories]

{expand:Detailed Test Scenarios}
[Put specific test data and edge cases here]
{expand}

(From commits: ...)
```

---

## Word Count Guidelines

| Section | Target Words | Max Words |
|---------|--------------|-----------|
| What Changed | 50-100 | 150 |
| Affected Functions | 20-40 | 60 |
| Test Suggestions | 100-200 | 300 |
| **TOTAL (excluding expand)** | **200-400** | **500** |

---

## Summary Checklist

Before posting to Jira, verify:
- [ ] NO title like "Test Documentation for MD-XXXXX"
- [ ] Total word count < 500 (excluding expand sections)
- [ ] Test Suggestions has 5-15 items max (not 20+)
- [ ] Grouped related tests instead of listing every case
- [ ] Detailed test data moved to {expand} sections
- [ ] Focused on high-level test categories, not individual cases
