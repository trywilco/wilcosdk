# github_commit_file

Category: Github
Type: Action

### Description

**Type**: action

Commit a single file to the main branch of the user's repository

## Params

- **file:** the file to commit (from the tests folder)
- **path:** where to copy this file too in the user's repository
- **message** commit message to show

## Result

No additional info is added to the global payload outputs.

## Usage Example

```yaml
  - actionId: github_commit_file
    params:
      file: "info.txt"
      path: "."
      message: "New file to commit"
```

In this example, we put the info file in the root directory

## Relevant Triggers

All triggers
