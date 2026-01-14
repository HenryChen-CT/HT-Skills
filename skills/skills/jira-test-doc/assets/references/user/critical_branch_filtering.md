# CRITICAL: Branch Filtering Rule

## ⚠️ MANDATORY REQUIREMENT

**Commits MUST be found from branches containing the ticket keyword (case-insensitive).**

## Quick Process

For ticket `MD-17127`:

```bash
# 1. Find branch (case-insensitive)
git branch -a | grep -i "md-17127"
# Output: MD-17127, remotes/origin/MD-17127

# 2. Get commits from that branch ONLY
git log MD-17127 --oneline --no-merges | head -20

# 3. Analyze each commit
git show <commit-hash>
```

## ❌ NEVER Do This

```bash
# DON'T use --grep with --all (searches all branches)
git log --grep="MD-17127" --all --oneline  # ❌ WRONG
```

## ✅ Always Do This

```bash
# DO use branch-specific search
git branch -a | grep -i "md-17127"          # ✅ Find branch
git log <branch-name> --oneline --no-merges # ✅ Get commits
```

## Why This Matters

- Ensures only ticket-related commits are analyzed
- Avoids documenting unrelated merged changes
- Maintains accuracy and context

## Edge Case: No Branch Found

If no branch exists:
- Use `git log --grep="<ticket>" --all --oneline` as fallback
- Note this in the documentation output
