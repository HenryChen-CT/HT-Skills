# Troubleshooting Guide

# Troubleshooting

## Issue: Generated documentation is too technical

**Symptoms:**
- Documentation uses terms like "service", "endpoint", "query"
- QA team asks "What does this mean?"
- Documentation reads like code comments

**Solutions:**
1. Manually edit the generated documentation before posting
2. Add custom knowledge with project-specific term mappings:
   ```bash
   skill-creator add-skill --pwd "..." --title "Project Terms" --content "
   - BOAllergenService = Allergen management system
   - ItemVersionController = Item editing feature
   - RecipeWebService = Recipe management
   "
   ```
3. Provide feedback in the skill's context for better future translations
4. Ask the skill to regenerate with "explain it like I'm a non-technical user"

## Issue: Test scenarios are too generic

**Symptoms:**
- Scenarios like "Test the feature works"
- No specific steps or expected results
- Misses important edge cases

**Solutions:**
1. Ensure Jira tickets have detailed acceptance criteria
2. Write commit messages that explain the WHY and context
3. Manually add specific edge cases after generation
4. Add examples to the skill:
   ```bash
   skill-creator add-skill --pwd "..." --title "Recipe Testing Patterns" --content "
   When testing recipe changes always include:
   - Test with 0 components
   - Test with 1 component
   - Test with 10+ components
   - Test with deleted components
   - Test nutrition recalculation
   "
   ```

## Issue: Some commits are missed

**Symptoms:**
- Important changes not included in documentation
- Commit count doesn't match expectations
- Documentation feels incomplete

**Solutions:**
1. Check commit message format - does it include the ticket number?
   - Required format: "MD-12345" somewhere in commit message
   - Case-sensitive matching
2. Try manual commit specification:
   ```bash
   /jira-test-doc MD-17127 --commits=a1b2c3d,e4f5g6h,i7j8k9l
   ```
3. Check if commits are in a different branch:
   ```bash
   git log --grep="MD-17127" --all --oneline
   ```
4. Increase search limit (default is 20):
   ```bash
   /jira-test-doc MD-17127 --limit=50
   ```

## Issue: Cannot post to Jira

**Symptoms:**
- Error: "Failed to post comment"
- Error: "Jira API authentication failed"
- Error: "Permission denied"

**Solutions:**
1. Verify Jira MCP tool is configured in Claude Code settings
2. Check authentication credentials are valid:
   - Jira URL is correct
   - API token is not expired
   - Username/email is correct
3. Verify you have permission to comment on the ticket:
   - Check ticket permissions in Jira
   - Ask project admin for comment permissions
4. Use  to generate locally and post manually:
   ```bash
   /jira-test-doc MD-17127 --dry-run
   ```
   Then copy-paste the output to Jira

## Issue: Skill is slow

**Symptoms:**
- Takes 2+ minutes to generate documentation
- Times out before completion
- Progress seems stuck

**Solutions:**
1. Reduce commit search limit:
   ```bash
   /jira-test-doc MD-17127 --limit=10
   ```
2. Skip detailed file analysis:
   ```bash
   /jira-test-doc MD-17127 --quick
   ```
3. Check network connectivity to Jira
4. Try with a simpler ticket first to verify it works

## Issue: Documentation format is wrong

**Symptoms:**
- Jira formatting is broken
- Bullets don't render correctly
- Headers are plain text

**Solutions:**
1. Ensure using Jira markdown format (not GitHub markdown)
2. Copy-paste into Jira's "visual editor" mode, not "text" mode
3. Use the  flag if posting to Confluence:
   ```bash
   /jira-test-doc MD-17127 --format=confluence
   ```

## Issue: Can't find skill after creation

**Symptoms:**
-  command not recognized
- Skill doesn't show in list

**Solutions:**
1. Restart Claude Code to reload skills
2. Verify skill was created in correct location:
   ```bash
   ls ~/.claude/skills/jira-test-doc/
   ```
3. Check SKILL.md file exists and is valid
4. Try full path:
   ```bash
   /Users/YOUR_USERNAME/.claude/skills/jira-test-doc
   ```