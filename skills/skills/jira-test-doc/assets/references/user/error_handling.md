# Error Handling

# Error Handling

The skill gracefully handles common errors:

## Ticket Not Found
```
Error: Jira ticket MD-99999 not found.
Please verify the ticket number and try again.
```

## No Commits Found
```
Warning: No commits found with "MD-17127" in the message.
Would you like to manually specify commit hashes? (y/n)
```

## No Meaningful Changes
```
Found 3 commits but they only contain:
- Configuration changes
- Code formatting
- Documentation updates

These don't require QA testing. Continue anyway? (y/n)
```

## Jira API Failure
```
Error: Cannot connect to Jira API.
I've generated the documentation locally.
Would you like to see it? (y/n)
```

## Git Repository Issues
```
Error: Not a git repository or git is not installed.
Please ensure you're in a git repository.
```

## Permission Issues
```
Error: You don't have permission to comment on ticket MD-17127.
The documentation has been generated and copied to clipboard.
```