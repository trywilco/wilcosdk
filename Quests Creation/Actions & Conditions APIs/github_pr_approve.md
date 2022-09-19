# github_pr_approve

Category: Github
Description: Approve the PR and add comment on behalf of a bot.
Type: Action

## Description

**Type**: Action

Approve the PR and add comment on behalf of a bot

## Params

- **person:** Name of the bot. e.g., `keen` or `lucca`
- **message:** The comment text
    
    [Text Formatting](../Text%20Formatting.md)
    

## Result

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:
- actionId: github_pr_approve
  params:
    person: keen
    message: "Nailed it! Excellent job @${user.githubuser}! You can now merge the PR."
```

The `github_pr_approve` action is used to approve the PR and let user know he should merge it. The message is sent on behalf of the bot `keen`

## Relevant Triggers

- `github_pr_lifecycle_status`