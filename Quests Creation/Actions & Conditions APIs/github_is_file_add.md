# github_is_file_add

Category: Github
Description: Check if specified files was added as part of PR changes.
Type: Condition

## Description

**Type**: Condition

Check if specified files was added as part of PR changes

## Params

- **fileName:** file path in the repository

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: github_is_file_added
    paramsFramework:
      node:
        fileName: backend/package-lock.json
  then:
    ...
```

The `github_is_file_added` condition is used to check if the file `backend/package-lock.json` was added for `Node` backend. For other frameworks, the condition will return `false`.

## Relevant Triggers

- `github_pr_lifecycle_status`
