---
name: production-bug-investigation
description: Use when investigating production errors, analyzing stack traces, tracing NPEs or runtime exceptions, diagnosing data-related bugs, or generating bug investigation reports. Triggers include error logs, trace IDs, stack traces, 500 errors, NullPointerException, and "why did this fail" questions.
---

# Production Bug Investigation

## Overview

Systematic methodology for investigating production bugs by combining **code analysis** and **data verification** in parallel, then tracing architecture to understand root cause. The key insight: most production bugs are not just code OR data problems — they're the interaction between code assumptions and unexpected data states.

## When to Use

- User shares an error trace / stack trace / log entry
- Production 500 error or runtime exception to diagnose
- "Why did this fail?" questions with a trace ID or error log
- NPE, ClassCastException, or data-related runtime errors
- Need to generate a bug investigation report

## When NOT to Use

- Build/compile errors (use compiler output directly)
- Performance issues without errors (use profiling tools)
- Feature requests or design discussions

## Investigation Flow

```
Parse Trace → Extract Key Info
        ↓
   ┌────┴────┐
   ↓         ↓
Read Code   Query Data    ← PARALLEL
   ↓         ↓
   └────┬────┘
        ↓
  Identify Root Cause
        ↓
  Check Change History   ← Understand timeline
        ↓
  Trace Architecture     ← Understand WHY data is in this state
        ↓
  Analyze Impact Scope   ← What else is affected?
        ↓
  Document Findings      ← Report with reproduction steps
```

## Phase 1: Parse the Trace

Extract ALL key information from the error log before doing anything else:

| Extract | Example |
|---|---|
| **Service** | `internal-recipe-service` |
| **API/Action** | `PUT /bo/menu/:id/dashboard/menu-items/:itemVersionId/sub-items` |
| **Error type** | `NullPointerException` |
| **Error message** | `Cannot read field "sodiumMg" because "nutritionFact" is null` |
| **Crash location** | `BOMenuDashboardUtilService.buildItemPart2:360` |
| **Entity IDs** | menu ID, item version IDs from URL path and DB queries |
| **Timestamp** | `2026-03-09T14:11:15Z` |
| **DB queries in log** | Collections queried, filters used, documents returned |
| **Caller** | `client=recipe-site` |

**Key insight**: Production logs often contain DB query details (collection, filter, returnedDocs). These reveal the exact data the code was working with at crash time.

## Phase 2: Parallel Code + Data Investigation

**Do these simultaneously, not sequentially.**

### Code Side
1. Locate the crash file and read the crash line with surrounding context (±30 lines)
2. Trace the call chain — read the calling method to understand the data flow
3. Identify the null-safety gap — what assumption does the code make about data?

### Data Side
1. Query the exact entities involved using IDs from the trace
2. Check the field that the code expected to be non-null
3. Check related entities (e.g., BOM line items, sub-items)

**Use MongoDB MCP tools (or equivalent) to query production data directly. Always read-only.**

## Phase 3: Root Cause Identification

Cross-reference code assumptions with actual data state:

```
Code assumes: nutritionFact != null (no null check)
Data reality: nutritionFact IS null for HDR_CONSUMABLE_ITEM without nutrition
Gap: Code handles INGREDIENT (emptyNutritionFact) and RECIPE (emptyNutritionFact)
     but not HDR_CONSUMABLE_ITEM (returns null)
```

**Pattern matching**: Compare the broken code path with similar working paths. Often the bug is an inconsistency — one branch handles a case that another branch doesn't.

## Phase 4: Change History Analysis

Check audit logs / change history collections to understand the **timeline**:

1. When was the entity created?
2. Was the missing field ever populated?
3. When was it populated (before or after the error)?
4. Who made changes and what kind?

This answers "was the data always broken, or did it change?" and often reveals whether the fix was a data fix (someone manually corrected it) or the bug is still latent.

**Common audit collections**: `*_change_logs`, `*_histories`, `*_audit`, or check `updated_time` / `created_time` fields on documents.

## Phase 5: Architecture Tracing

For data-related bugs, understand the **data lifecycle**:

1. **Where is the field written?** — Find all code paths that set/save the field
2. **When is it triggered?** — Creation? Publish? Async job? Manual action?
3. **What are the prerequisites?** — Does it depend on linked entities existing?
4. **What DOESN'T trigger it?** — Gaps in the trigger chain

This reveals whether the bug is:
- **Code defect**: Missing null check (fix the code)
- **Architecture gap**: Field never gets populated in certain workflows (fix the workflow or make code defensive)
- **Data corruption**: Field was unexpectedly removed (investigate the cause)

## Phase 6: Impact Scope Analysis

Check if the same bug pattern affects other types or paths:

1. Find all callers of the broken method
2. Check if sibling types (e.g., INGREDIENT, RECIPE, PACKAGED) have the same vulnerability
3. Check recursive/nested paths — can the bug be triggered indirectly?

**Template**: "Method X returns null for type A. Does it also return null for types B, C, D? Are there callers that don't null-check the result?"

## Phase 7: Bug Report Generation

Structure the report with these sections:

```markdown
## Basic Info (table: trace ID, time, service, API, error, impact)
## Request Context (entity IDs, caller, involved data)
## Stack Trace (key frames only)
## Root Cause Analysis
  - Direct cause (what line crashed and why)
  - Code defect (the actual bug in code)
  - Impact scope (other affected paths)
## Data Background (why the data was in this state)
## Involved Data (table of affected entities)
## Data Timeline (from change history, chronological)
## Reproduction Method
  - Trigger condition
  - Step-by-step reproduction
  - Quick verification queries
  - Why it's easy/hard to reproduce
## Fix Recommendation (minimal code change)
```

## Common Mistakes

| Mistake | Better Approach |
|---|---|
| Reading code without checking data | Always parallel — code + data together |
| Assuming current data = crash-time data | Check timestamps; data may have been fixed post-incident |
| Stopping at "found the NPE line" | Trace WHY the data was null (architecture) |
| Only checking the direct crash type | Check sibling types and recursive paths for same pattern |
| Proposing data fix without code fix | If code can't handle null, fix the code — data is the symptom |
| Writing report without reproduction steps | Always include concrete reproduction method |

## Quick Reference: Investigation Checklist

- [ ] Parse trace: service, API, error, IDs, timestamp, DB queries
- [ ] Read crash code with ±30 lines context
- [ ] Query involved entities in production (read-only)
- [ ] Cross-reference: what does code assume vs what data shows?
- [ ] Check change history / audit logs for timeline
- [ ] Trace field lifecycle: where written, when triggered, what gaps
- [ ] Analyze impact scope: sibling types, callers, recursive paths
- [ ] Document reproduction steps with concrete queries
- [ ] Generate structured report
