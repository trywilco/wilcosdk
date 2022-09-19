# github_is_user_valid

Category: Github
Description: Check if username exists in Github
Type: Condition

## Description

**Type**: Condition

Check if username exists in Github

## Params

- **githubUserName:** Github username to verify

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if: 
  conditions:
    - conditionId: user_check_authentication_exists
      name: user_authentication
      params: 
        authType: 'github'
    - conditionId: github_is_user_valid
      params:
        githubUserName: "${outputs.user_authentication.value.nickname}"
```

The `github_is_user_valid` condition uses the result of `user_check_authentication_exists` and checks if it is a valid Github user name.

## Relevant Triggers

All triggers