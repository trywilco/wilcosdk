# github_is_repo_collaborator

Category: Github
Description: Check if user accepted the invitation for his repo. 
Type: Condition

## Description

**Type**: Condition

Check if user accepted the invitation for his repo. 

## Params

No params required as condition user Github username and Github repo name stored in  `user`

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: github_is_repo_collaborator
  then:
    ...
```

## Relevant Triggers

All triggers
