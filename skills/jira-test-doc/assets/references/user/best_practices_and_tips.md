# Best Practices and Tips

# Best Practices

## For Developers

### 1. Run After Completing Ticket Work
Generate documentation when all commits for the ticket are done. This ensures comprehensive coverage.

### 2. Review Before Posting
Always review the generated documentation for accuracy. The AI does its best but may miss context or use incorrect terminology for your specific domain.

### 3. Add Context for Edge Cases
If the generated scenarios miss important edge cases, manually add them before posting to Jira.

### 4. Link to Related Tickets
If your change affects or depends on other tickets, mention them in the documentation.

### 5. Update Commit Messages
Write clear commit messages that explain WHY you made changes, not just WHAT you changed. This helps generate better documentation.

**Good commit message:**
```
MD-17127 Fix allergen deletion to update recipes

When an allergen is deleted, we need to update all recipes that use it
to remove the allergen from their allergen lists. This prevents showing
incorrect allergen information to users.
```

**Poor commit message:**
```
MD-17127 fix bug
```

## For QA Teams

### 1. Use as Starting Point
Generated scenarios are suggestions, not exhaustive test plans. Use them as a foundation for your testing strategy.

### 2. Verify Expected Results
If expected behavior is unclear, confirm with the developer before starting tests.

### 3. Add Exploratory Tests
Use generated scenarios as smoke tests, then expand with exploratory testing.

### 4. Update if Implementation Changes
If the implementation changes during testing (bug fixes, requirement changes), ask the developer to regenerate documentation.

### 5. Report Documentation Issues
If the documentation is consistently inaccurate or missing important details, provide feedback to improve the skill.

## Tips for Better Documentation

### Tip 1: Write Detailed Jira Tickets
The better your Jira ticket describes requirements and acceptance criteria, the better the generated documentation will be.

### Tip 2: Use Descriptive Branch Names
If using feature branches, include the ticket number in the branch name.

### Tip 3: Commit Often with Context
Make focused commits with clear messages rather than large commits with vague messages.

### Tip 4: Tag Important Commits
If some commits are more important than others, mention that in the commit message.

### Tip 5: Review Generated Docs Together
For complex features, have the developer and QA review the generated documentation together to ensure alignment.