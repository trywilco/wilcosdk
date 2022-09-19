# github_is_one_of_files_modified

Category: Github
Description: Check if one of specified files was modified as part of PR changes
Type: Condition

## Description

**Type**: Condition

Check if one of specified files was modified as part of PR changes

## Params

- **fileNames:** files paths in the repository

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: github_is_one_of_files_modified
    params:
      fileNames:
      - backend/readme.md
      - frontend/readme.md
      - readme.md
  then:
    ...
```

The `github_is_one_of_files_modified` condition is used to check if one of the `[reamde.md](http://reamde.md)` files in the repository was modified in the PR

## Relevant Triggers

- `github_pr_lifecycle_status`
