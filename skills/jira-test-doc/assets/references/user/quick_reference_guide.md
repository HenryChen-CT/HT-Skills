# Quick Reference Guide

# Quick Reference Guide - jira-test-doc

## Quick Command

```bash
/jira-test-doc <TICKET_ID>
```

Example:
```bash
/jira-test-doc MD-17127
```

## What It Does

1. ✅ Fetches Jira ticket details
2. ✅ Finds branch containing ticket keyword (case-insensitive)
3. ✅ Finds commits from that specific branch
4. ✅ Analyzes code changes and filtering logic
5. ✅ Generates test documentation in ENGLISH
6. ✅ Posts to Jira as a comment

## Output Format Checklist

Your test documentation will include:

### 【What Changed】
- ✅ Brief summary (1-2 sentences)
- ✅ Main changes as numbered list (#)
- ✅ Filtering logic details (use {expand} if complex)
- ✅ User-friendly language
- ✅ Line breaks between sections

### 【Affected Functions】
- ✅ Numbered list (#) of affected features/pages
- ✅ Clear, specific function names

### 【Test Suggestions】
- ✅ Numbered list (#) of test scenarios
- ✅ ONLY describe test actions (NO expected results)
- ✅ Cover positive, negative, and edge cases
- ✅ Include filter-related test cases

## Quality Checklist

Before posting, verify:
- ✅ ALL content is in English
- ✅ Using numbered lists (#), NOT bullets (-)
- ✅ Proper line breaks between sections
- ✅ Filtering logic is included in "What Changed"
- ✅ Complex details are in {expand} sections
- ✅ Test suggestions have NO expected results
- ✅ Technical terms are translated to user-friendly language

## Common Issues

### Issue: Documentation in Chinese
**Solution**: Regenerate and explicitly request English

### Issue: No commits found
**Solution**: Check if branch exists with `git branch -a | grep -i "<ticket-id>"`. Commits are ONLY searched from branches containing the ticket keyword, not from all branches.

### Issue: Wrong commits analyzed
**Solution**: Verify you're on the correct branch. The skill only analyzes commits from branches whose name contains the ticket keyword (case-insensitive).

### Issue: Missing filtering logic
**Solution**: Review code for filter conditions (eq, ne, in, DORMANT, deleted, effective)

### Issue: Test suggestions too verbose
**Solution**: Remove "should do X" - just describe the action

### Issue: No line breaks
**Solution**: Add blank lines between sections and list items

## Time-Saving Tips

1. **Run immediately after commits** - Fresh context helps
2. **Review code first** - Understand filtering logic before generating
3. **Use {expand}** - Don't overwhelm main text with details
4. **Let QA know** - Tag them when documentation is posted

## Example Flow

```bash
# After finishing your work on a ticket
git add .
git commit -m "MD-12345 Description"
git push

# Generate test documentation
/jira-test-doc MD-12345

# Review output
# Confirm to post to Jira
# Done! QA is notified
```

## Search Documentation

Need help? Search the skill docs:

```bash
# Search for specific topics
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "filtering logic"
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "formatting"
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "examples"
```
