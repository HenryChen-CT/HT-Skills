# Implementation Details

# Implementation Details

## Required Tools
- **Bash**: For git commands and shell operations
- **Read**: For reading code files and analyzing changes
- **Jira MCP**: For fetching tickets and posting comments
  - mcp__jira__jira_get: Fetch ticket information
  - mcp__jira__jira_post: Post comments to tickets
- **Grep**: For searching code patterns
- **Glob**: For finding related files

## Git Commands Used

### IMPORTANT: Branch Filtering Requirement
**Commits MUST be found from branches that contain the ticket keyword (case-insensitive, fuzzy match).**

For example, for ticket MD-17127:
1. First find branches containing the ticket keyword: `git branch -a | grep -i "md-17127"`
2. Then get commits from that branch: `git log <branch-name> --oneline --no-merges`
3. Analyze only commits from the matched branch, NOT from `--all` or `--grep`

This ensures we only document changes that are actually part of the ticket's development branch.

### Common Git Commands
```bash
# Step 1: Find branch containing the ticket keyword (case-insensitive)
git branch -a | grep -i "md-17127"
# Example output: MD-17127, remotes/origin/MD-17127

# Step 2: Get commits from the specific branch
git log MD-17127 --oneline --no-merges | head -20

# Get commit details
git show <commit-hash> --stat

# Get full diff for a commit
git show <commit-hash>

# Get specific file changes
git show <commit-hash> -- path/to/file.java

# Get current branch
git branch --show-current

# Get commit message
git log -1 --format=%B <commit-hash>
```

## File Analysis Strategy
1. **Backend Files**: Look for Service, Controller, Repository patterns
2. **Frontend Files**: Look for components, pages, API calls
3. **Database Files**: Look for migrations, schema changes
4. **Config Files**: Usually skip for test documentation

## Business Impact Mapping
- Service changes → System functions
- Controller changes → User workflows/features
- Frontend component changes → Page sections
- API changes → Feature availability
- Database changes → Data integrity/performance

## Documentation Generation Algorithm
1. **Parse Jira ticket**: Extract requirements and acceptance criteria
2. **Collect commits**: Find all related commits
3. **Analyze changes**: Group by file type and business domain
4. **Map to features**: Translate technical files to business features
5. **Generate scenarios**: Create test cases based on:
   - Requirements (from Jira)
   - Code changes (from commits)
   - Common patterns (from skill knowledge)
6. **Format output**: Convert to Jira markdown format