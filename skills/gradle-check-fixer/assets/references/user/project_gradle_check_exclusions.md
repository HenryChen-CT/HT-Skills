# Project: Gradle Check Exclusions

## Master Data Management Project

### Modules to Exclude from Code Quality Checks

The following modules should be **excluded** from code quality checks (checkstyle, PMD, SpotBugs) when running `./gradlew check`:

1. **backend/common-library**
2. **backend/domain-library**
3. **backend/service-common-library**

### Rationale

These library modules contain shared utilities and domain models that don't require the same level of code quality enforcement as service modules.

### When Running Gradle Check Fixer

When analyzing gradle check results or attempting to fix violations:
- **Ignore** all violations from these three library modules
- **Do not attempt to fix** any issues in these excluded modules
- Only focus on violations from service modules (e.g., `internal-recipe-service`, `recipe-service-v2`, etc.)
- When generating fix reports, exclude these modules from the report

### Example Command

```bash
./gradlew check
# Ignore violations from:
# - backend/common-library
# - backend/domain-library
# - backend/service-common-library
```

### Implementation Note

When the skill processes gradle check output:
1. Filter out any errors/warnings from these three modules
2. Only report issues from non-excluded modules
3. Only attempt fixes on non-excluded modules
