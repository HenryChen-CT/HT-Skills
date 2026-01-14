---
name: gradle-check-fixer
description: Automatically run gradle check on selected services and fix Checkstyle, PMD, and SpotBugs errors with high confidence. Only fixes errors with absolute certainty - uncertain fixes are reported for user review. Generates concise fix reports. Use when user requests gradle check, code style fixes, or mentions checkstyle/PMD/spotbugs errors.
allowed-tools: Read, Write, Edit, Bash, Glob, AskUserQuestion
---

# Gradle Check Fixer

Automatically runs `gradle check` on selected services and fixes errors with absolute confidence. Uncertain issues are reported for manual review.

## When to Use

This skill should be activated when:
- User requests to run `gradle check`
- User wants to fix code style issues
- User mentions Checkstyle, PMD, or SpotBugs errors
- User asks to prepare code for commit (if your company requires gradle check before commits)

## Key Features

1. **Smart Service Selection**:
   - Supports both single and multiple service selection
   - Caches service list for faster subsequent runs
   - Auto-scans from `settings.gradle.kts` on first use

2. **Comprehensive Error Detection**:
   - Checkstyle violations
   - PMD rule violations
   - SpotBugs issues

3. **Safe Automated Fixing**:
   - Only fixes errors with 100% confidence
   - Reports uncertain errors for user review
   - Never guesses or makes risky changes
   - Generates detailed fix report after completion

4. **Efficient Execution**:
   - Serial execution (one service at a time)
   - Persistent caching to avoid re-scanning
   - Only rescans when explicitly requested or cache is stale

## Workflow

### First Time Usage

1. **Initialize**: Automatically scan `settings.gradle.kts` to detect all services
2. **Cache**: Store service list in `~/.claude/gradle-check-fixer/services-cache.json`
3. **Select**: Present user with service selection (supports multi-select)
4. **Execute**: Run gradle check and fix errors for each selected service

### Subsequent Usage

1. **Load Cache**: Read cached service list (skip scanning)
2. **Select**: Present user with service selection
3. **Execute**: Run gradle check and fix errors

### Manual Refresh

If user requests to refresh service list or if project structure changes:
1. Delete cache file
2. Re-scan `settings.gradle.kts`
3. Update cache

## Implementation Details

### Service Detection

Parse `settings.gradle.kts` to extract all `include()` statements:

```kotlin
include(
    "backend:common-library",
    "backend:internal-recipe-service",
    "frontend:recipe-site",
    "tool:email-library",
)
```

Extract services from:
- `backend/*`
- `frontend/*`
- `tool/*`

### Cache Structure

`~/.claude/gradle-check-fixer/services-cache.json`:

```json
{
  "projectPath": "/Users/sunrise/IdeaProjects/md_v2/master-data-management",
  "lastScanned": "2026-01-07T17:15:00Z",
  "services": [
    {
      "name": "internal-recipe-service",
      "path": "backend:internal-recipe-service",
      "category": "backend"
    },
    {
      "name": "recipe-site",
      "path": "frontend:recipe-site",
      "category": "frontend"
    }
  ]
}
```

### Error Parsing

**Checkstyle Error Format**:
```
[ant:checkstyle] [ERROR] /path/to/File.java:95:9: Variable 'name' can be moved inside the block at line '96'. [MoveVariableInsideIf]
```

**PMD Error Format**:
```
/path/to/File.java:123: SomeRule: Description of the violation
```

**SpotBugs Error Format**:
```
[ERROR] High: Description [CLASS_NAME] At File.java:[line 123]
```

### Execution Strategy

For each selected service:

1. **Run Check**:
   ```bash
   cd /path/to/project
   ./gradlew :backend:service-name:check --continue
   ```

2. **Parse Output**:
   - Capture stderr and stdout
   - Extract error file path, line number, and violation description
   - Identify error type (Checkstyle/PMD/SpotBugs)

3. **Fix Errors (High Confidence Only)**:
   - Categorize each error by confidence level
   - **Auto-fix (100% confidence)**:
     - Remove unused imports
     - Fix whitespace/formatting
     - Move variable declarations (MoveVariableInsideIf)
     - Add missing @Override annotations
     - Fix simple naming conventions
     - Remove redundant modifiers
   - **Report for review (uncertain)**:
     - Logic changes requiring business context
     - Complex refactoring
     - Performance-related changes
     - Null safety that might affect behavior
     - Any change that could introduce bugs

4. **Verify**:
   - Re-run gradle check
   - If errors remain, repeat steps 2-3
   - Max 5 iterations per service

5. **Generate Fix Report**:
   - **Fixed Issues**: List of auto-fixed errors with file:line references
   - **Uncertain Issues**: Errors requiring manual review with explanations
   - **Final Status**: Build success/failure with statistics
   - **Changes Summary**: Concise summary of all code modifications

## Fix Confidence Classification

### High Confidence (Auto-Fix) ✅

These errors are fixed automatically without user confirmation:

| Error Type | Checkstyle Rule | Example | Why Safe |
|-----------|----------------|---------|----------|
| Unused imports | UnusedImports | `import java.util.List;` (unused) | No behavior change |
| Redundant modifiers | RedundantModifier | `public interface { public void m(); }` | No behavior change |
| Move variable inside if | MoveVariableInsideIf | Move declaration closer to usage | No behavior change |
| Whitespace | WhitespaceAround, WhitespaceAfter | Missing space after comma | No behavior change |
| Missing @Override | MissingOverride | Method overrides but no annotation | No behavior change |
| Empty block | EmptyBlock | `if (x) {}` → `if (x) { }` or remove | Safe pattern |
| Final local variable | FinalLocalVariable | Add `final` to never-reassigned vars | Makes code safer |

### Medium Confidence (Report for Review) ⚠️

These errors require user review:

| Error Type | Rule | Why Uncertain |
|-----------|------|---------------|
| Magic numbers | MagicNumber | May have business meaning |
| Complex conditionals | CyclomaticComplexity | Refactoring needs domain knowledge |
| Long method | MethodLength | Breaking up requires understanding flow |
| Too many parameters | ParameterNumber | API design decision |
| Null checks | NullPointerException risks | May affect business logic |
| Exception handling | EmptyCatchBlock with logic | May hide intentional behavior |

### Low Confidence (Never Auto-Fix) ❌

These are always reported, never fixed automatically:

- Any change affecting business logic
- Database/API interactions
- Security-related code
- Performance optimizations requiring profiling
- Architectural changes

## Fix Report Format

After running gradle check, generate a report in this format:

```markdown
# Gradle Check Fix Report

## Service: backend:internal-recipe-service

### ✅ Auto-Fixed Issues (3)

1. **UnusedImports** - BOItemService.java:15
   - Removed: `import java.util.HashMap;`

2. **MoveVariableInsideIf** - BOItemService.java:95
   - Moved `itemVersionMap` declaration inside if block

3. **WhitespaceAfter** - BOItemService.java:120
   - Added space after comma in parameter list

### ⚠️ Issues Requiring Review (2)

1. **MagicNumber** - BOPriceCalculator.java:45
   ```java
   double tax = price * 0.13;  // Magic number: 0.13
   ```
   **Suggestion**: Extract to named constant `TAX_RATE`
   **Why uncertain**: Tax rate may be business-specific, needs verification

2. **CyclomaticComplexity** - BOValidator.java:78
   - Method `validateItem()` has complexity 15 (max: 10)
   **Suggestion**: Extract validation logic into separate methods
   **Why uncertain**: Requires understanding validation flow

### 📊 Summary

- **Total errors found**: 5
- **Auto-fixed**: 3 (60%)
- **Needs review**: 2 (40%)
- **Build status**: ✅ SUCCESS (after fixes)

### 📝 Code Changes

**Modified files**: 3
- `BOItemService.java` - 2 fixes (imports, variable placement)
- `BOPriceCalculator.java` - 1 fix (whitespace)

**Lines changed**: 5 additions, 3 deletions
```

## User Interaction

### Service Selection

Use `AskUserQuestion` tool to present service selection:

```
Question: "Which service(s) do you want to check?"
Options:
  - internal-recipe-service (backend)
  - recipe-site (frontend)
  - email-library (tool)
  - [All services]
Multi-select: true
```

### Cache Refresh

If user mentions:
- "refresh service list"
- "rescan services"
- "update service cache"

Then delete cache and rescan.

## Implementation Guidelines

### Error Classification Algorithm

For each detected error, follow this decision tree:

```
1. Is it a pure syntax/style issue with zero behavior change?
   YES → Auto-fix
   NO → Continue to 2

2. Does it require understanding business logic or domain knowledge?
   YES → Report for review
   NO → Continue to 3

3. Could the fix potentially introduce bugs or change behavior?
   YES → Report for review
   NO → Continue to 4

4. Is the fix pattern well-established and safe?
   YES → Auto-fix
   NO → Report for review
```

### Auto-Fix Implementation Examples

**Example 1: Unused Import (Safe)**
```java
// Before
import java.util.HashMap;  // ← unused
import java.util.List;

public class Foo {
    private List<String> items;
}

// After - just remove the unused import
import java.util.List;

public class Foo {
    private List<String> items;
}
```

**Example 2: MoveVariableInsideIf (Safe)**
```java
// Before
Map<String, Item> itemMap = items.stream()...;
if (needUpdate) {
    itemMap.forEach(...);
}

// After - move declaration inside if
if (needUpdate) {
    Map<String, Item> itemMap = items.stream()...;
    itemMap.forEach(...);
}
```

**Example 3: MagicNumber (Unsafe - Report)**
```java
// Do NOT auto-fix this:
double price = basePrice * 1.13;  // What is 1.13?

// Report: "Magic number 1.13 - could be tax rate, markup, etc.
// Suggest: Extract to named constant after confirming meaning"
```

### Report Generation Steps

1. **Track all changes**: Keep a list of every modification made
2. **Categorize errors**: Separate fixed vs. needs-review
3. **Format report**: Use the template format shown above
4. **Include context**: For uncertain issues, explain WHY uncertain
5. **Provide suggestions**: Offer actionable next steps

## Error Handling

### Build Errors

If gradle check fails due to compilation errors (not style issues):
1. Report the compilation error
2. Ask user if they want to:
   - Fix compilation errors first
   - Skip this service
   - Abort

### Max Attempts Reached

After 5 failed fix attempts:
1. Report remaining errors
2. Show error report file location
3. Ask if user wants to continue with next service

### Permission Issues

If unable to write to cache directory:
1. Fall back to scanning every time
2. Warn user about performance impact

## Advanced Features

### Parallel Service Detection (Future)

Currently uses serial execution. Could be extended to:
- Run checks in parallel
- Aggregate errors
- Fix all at once

### Custom Rules

Allow users to specify:
- Which checks to run (Checkstyle only, PMD only, etc.)
- Custom fix patterns
- Exclusion rules

### Integration with Git

- Auto-commit after successful fixes
- Create branch for fixes
- Generate commit message based on fixes applied

## Tips for Users

1. **Review the fix report**: Check what was auto-fixed and what needs manual review
2. **Trust the auto-fixes**: High-confidence fixes are safe and well-tested
3. **Carefully review uncertain issues**: These require your domain knowledge
4. **Run on clean working directory**: Commit or stash changes before running
5. **Start small**: Try on one service first to verify behavior
6. **Keep cache fresh**: Refresh when project structure changes
7. **Read the change summary**: Understand all code modifications before committing

## Limitations

1. **Conservative fixing**: Only fixes high-confidence issues (better safe than sorry)
2. **No guessing**: Will report uncertain issues rather than risk incorrect fixes
3. **Performance**: Serial execution can be slow for many services
4. **Java-specific**: Currently only supports Java projects with Gradle
5. **Manual review required**: Complex issues still need human judgment

## See Also

- [Checkstyle Documentation](https://checkstyle.sourceforge.io/)
- [PMD Rule Reference](https://pmd.github.io/)
- [SpotBugs Bug Descriptions](https://spotbugs.readthedocs.io/)
- Project-specific rules: `buildSrc/src/main/check/checkstyle.xml`
