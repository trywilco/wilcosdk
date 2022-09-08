# github_pr_comment

Category: Github
Description: Add comment on a PR on behalf of one the bots.
Type: Action

## Description

**Type**: Action

Add comment on a PR on behalf of one the bots

## Params

- **person:** Name of the bot. e.g., `head-of-rd` or `devops`
- **message:** The comment text
    
    [Text Formatting](../Text%20Formatting.md)
    

## Result

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:          
- actionId: github_pr_comment
  params:
    person: head-of-rd
    message: "On it, I'll review the changes right away."
```

The `github_pr_comment` action is used to add comment from `head-of-rd` letting user know that she will review the PR.

The example is taken from the `funnel-drop` quest:

[](https://github.com/trywilco/quest-funnel-drop/blob/main/steps/funneldrop_fixing_bug_pr.yml)

## Relevant Triggers

- `github_pr_lifecycle_status`