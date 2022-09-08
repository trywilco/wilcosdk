# github_pr_approve

Category: Github
Description: Approve the PR and add comment on behalf of a bot.
Type: Action

## Description

**Type**: Action

Approve the PR and add comment on behalf of a bot

## Params

- **person:** Name of the bot. e.g., `head-of-rd` or `devops`
- **message:** The comment text
    
    [Text Formatting](../Text%20Formatting.md)
    

## Result

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:
- actionId: github_pr_approve
  params:
    person: head-of-rd
    message: "Nailed it! Excellent job @${user.githubuser}! You can now merge the PR."
```

The `github_pr_approve` action is used to approve the PR and let user know he should merge it. The message is sent on behalf of the bot `head-of-rd`

The example is taken from the `funnel-drop` quest:

[https://github.com/trywilco/quest-funnel-drop/blob/main/steps/funneldrop_fixing_bug_pr.yml](https://github.com/trywilco/quest-funnel-drop/blob/main/steps/funneldrop_fixing_bug_pr.yml)

## Relevant Triggers

- `github_pr_lifecycle_status`