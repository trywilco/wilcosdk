# github_is_file_contains

Category: Github
Description: Check if file added in PR contains text that matches a regex
Type: Condition

## Description

**Type**: Condition

Check if file added in PR contains text that matches a regex

## Params

- **fileName:** file path in the repository
- **regex:** Regex string. Value is used as input to `RegExp` ******constructor

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: github_is_file_contains
    params:
      regex: license_key
    paramsFramework:
      node:
        fileName: backend/newrelic.js
      rails:
        fileName: backend/config/newrelic.yml
      python:
        fileName: backend/newrelic.ini
  then:
    ...
```

The `github_is_file_contains` condition is used to check if the `newrelic` file contains the string `license_key`.

## Relevant Triggers

- `github_pr_lifecycle_status`
