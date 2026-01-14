# Gradle Check Fix Report Template

This is a template for the fix report generated after running gradle check.

---

# Gradle Check Fix Report

**Project**: [project-path]
**Date**: [timestamp]
**Duration**: [elapsed-time]

---

## Service: [service-name]

### ✅ Auto-Fixed Issues ([count])

#### 1. **[Rule Name]** - [File.java]:[line]
- **What was fixed**: [Brief description]
- **Change**: [Before] → [After]

#### 2. **[Rule Name]** - [File.java]:[line]
- **What was fixed**: [Brief description]
- **Code snippet**:
  ```java
  // Before
  [old code]

  // After
  [new code]
  ```

---

### ⚠️ Issues Requiring Manual Review ([count])

#### 1. **[Rule Name]** - [File.java]:[line]
```java
[code snippet showing the issue]
```
**Issue**: [Describe the problem]
**Suggestion**: [Recommended fix]
**Why uncertain**: [Explain why this requires user judgment]
**Risk level**: [Low/Medium/High]

#### 2. **[Rule Name]** - [File.java]:[line]
```java
[code snippet showing the issue]
```
**Issue**: [Describe the problem]
**Suggestion**: [Recommended fix]
**Why uncertain**: [Explain why this requires user judgment]
**Risk level**: [Low/Medium/High]

---

### 📊 Summary

| Metric | Count |
|--------|-------|
| Total errors found | [X] |
| Auto-fixed | [X] ([Y]%) |
| Needs manual review | [X] ([Y]%) |
| Build status | ✅ SUCCESS / ❌ FAILED |
| Iterations | [X] |

---

### 📝 Code Changes Summary

**Modified files**: [count]

| File | Auto-fixes | Lines changed |
|------|-----------|---------------|
| [File1.java] | [X] fixes | +[A] -[D] |
| [File2.java] | [X] fixes | +[A] -[D] |

**Total changes**: +[additions] -[deletions] lines

---

### 🔍 Detailed Changes by File

#### [File1.java]
- **Line [X]**: Removed unused import `java.util.HashMap`
- **Line [Y]**: Moved variable declaration inside if block
- **Line [Z]**: Fixed whitespace after comma

#### [File2.java]
- **Line [X]**: Added missing @Override annotation

---

### 📋 Next Steps

1. ✅ Review auto-fixed changes (safe but good to verify)
2. ⚠️ **Action required**: Review [X] uncertain issues manually
3. Run tests to verify no behavior changes
4. Commit changes with message: "Fix Checkstyle/PMD/SpotBugs violations"

---

### 🛠️ Commands to Review Changes

```bash
# View changes in git
git diff

# Review specific file
git diff [path/to/File.java]

# Run tests
./gradlew :backend:service-name:test

# Commit if satisfied
git add .
git commit -m "Fix code style violations

Auto-fixed [X] Checkstyle/PMD/SpotBugs issues:
- Removed unused imports
- Fixed variable declarations
- Corrected whitespace

Reviewed [Y] uncertain issues - no changes needed

🤖 Generated with gradle-check-fixer skill"
```

---

## Notes

- All auto-fixes are non-behavioral changes
- Uncertain issues preserved code behavior intentionally
- Review the diff before committing
- Run full test suite to verify
