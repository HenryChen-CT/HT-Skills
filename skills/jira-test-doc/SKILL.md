---
name: |
  jira-test-doc
description: |
  Generate QA-friendly test documentation from Jira ticket and related commits, then post as Jira comment
---

# jira-test-doc

Generate QA-friendly test documentation from Jira ticket and related commits, then post as Jira comment

## CLI Commands

```bash
# Add user content
skill-creator add-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" [--title "Title" --content "Content"]|[--file=*.md]

# Search documentation
skill-creator search-skill --pwd "/Users/sunrise/.claude/skills/jira-test-doc" "query" [--mode=auto|chroma|fuzzy]

```

## User Skills

<user-skills baseDir="assets/references/user">
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
