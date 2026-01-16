---
name: |
  jira-test-doc
description: |
  Generate QA-friendly test documentation from Jira ticket and related commits, then post as Jira comment
---

# jira-test-doc

Generate QA-friendly test documentation from Jira ticket and related commits, then post as Jira comment

## ⚠️ CRITICAL: MANDATORY FIRST STEPS

**BEFORE generating ANY test documentation, you MUST:**

1. **Read ALL files** in `assets/references/user/` directory using Glob tool:
   ```
   Glob pattern: assets/references/user/*.md
   ```

2. **Read each file** found to understand all formatting and content rules

3. **Verify understanding** of these critical requirements:
   - ✅ 100% English (NO Chinese characters anywhere)
   - ✅ NO title header (do NOT start with "Test Documentation for MD-XXXXX")
   - ✅ Keep ENTIRE comment concise (target 300-500 words TOTAL, excluding {expand} sections)
   - ✅ Use numbered lists (#) NOT bullet points (-)
   - ✅ Test Suggestions = test scenarios ONLY (NO expected results)
   - ✅ Test Suggestions = 5-15 items MAX (group related tests, not 20+ individual cases)
   - ✅ Use {expand} for complex technical details and test data
   - ✅ Use 【】brackets for section titles: 【What Changed】【Affected Functions】【Test Suggestions】
   - ✅ Keep descriptions concise, focus on entry point and trigger scenario
   - ✅ When posting via Jira API: convert "#" to ADF `orderedList` structure (NOT text "#")

4. **DO NOT PROCEED** with content generation until steps 1-3 are complete

**Why this matters:** The rules in these files override any general knowledge about test documentation. Following them precisely is required for QA team compatibility.

## Setup

Set the environment variable once:

```bash
export JIRA_TEST_DOC_DIR="$HOME/.claude/skills/jira-test-doc"
```

Add this to your `~/.zshrc` or `~/.bashrc` to make it permanent.

## CLI Commands

```bash
# Add user content
skill-creator add-skill --pwd "$JIRA_TEST_DOC_DIR" [--title "Title" --content "Content"]|[--file=*.md]

# Search documentation
skill-creator search-skill --pwd "$JIRA_TEST_DOC_DIR" "query" [--mode=auto|chroma|fuzzy]

```

## User Skills

<user-skills baseDir="assets/references/user">
- 2026_01_16_jira_api_adf_format.md
- 2026_01_09_update_2_formatting_requirements.md
- 2026_01_09_update_3_test_suggestions_format.md
- 2026_01_09_update_language_and_filtering_requireme.md
- best_practices_and_tips.md
- cheat_sheet.md
- error_handling.md
- example_bug_fix_documentation.md
- example_new_feature_documentation.md
- formatting_best_practices.md
- implementation_details.md
- language_and_content_requirements.md
- language_guidelines_and_translations.md
- output_format.md
- quick_reference_guide.md
- quick_start_guide.md
- shell_aliases_optional.md
- simplified_example_bug_fix.md
- simplified_example_new_feature.md
- simplified_output_format.md
- simplified_workflow_guide.md
- skill_overview_and_purpose.md
- test_suggestions_format.md
- troubleshooting_guide.md
- update_summary_simplified_format.md
- usage_and_workflow.md
</user-skills>
