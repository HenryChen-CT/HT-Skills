# Shell Aliases (Optional)

# Shell Aliases for jira-test-doc

## Optional: Create Shell Alias

If you want to use this skill outside of Claude Code, you can create a shell alias.

### For bash (~/.bashrc or ~/.bash_profile)

```bash
# Add to your ~/.bashrc or ~/.bash_profile
alias jira-test-doc='claude /jira-test-doc'
```

### For zsh (~/.zshrc)

```bash
# Add to your ~/.zshrc
alias jira-test-doc='claude /jira-test-doc'
```

### Usage After Setting Alias

```bash
# Instead of opening Claude Code and typing /jira-test-doc
jira-test-doc MD-17127
```

## Reload Your Shell

After adding the alias, reload your shell:

```bash
# For bash
source ~/.bashrc

# For zsh
source ~/.zshrc
```

## Alternative: Function for More Control

```bash
# Add to your shell config file
jira-test-doc() {
    if [ -z "$1" ]; then
        echo "Usage: jira-test-doc <TICKET_ID>"
        echo "Example: jira-test-doc MD-17127"
        return 1
    fi
    claude "/jira-test-doc $1"
}
```

This provides helpful error messages if you forget the ticket ID.

## Note

These aliases are **optional**. The skill works perfectly within Claude Code using:
```
/jira-test-doc <TICKET_ID>
```
