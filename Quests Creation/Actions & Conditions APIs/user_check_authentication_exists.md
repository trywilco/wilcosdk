# user_check_authentication_exists

Category: General
Type: Condition

## Description

**Type**: Condition

Check if authentication info of specific type exists for the user. For example, check if Github auth info is set on the user.

## Params

- **authType:** Input string. One of `password`/`github`/`google`/`discord`

## Outputs

`value` is set on the condition outputs. It holds the user’s authentication info. 

Can be referenced in other blocks using `outputs.<condition_name>.value`

```json
{
  "value": { 
    "type": "<String>"
    "authId": "<String>"
    "name": "<String>"
    "nickname": "<String>"			 
  }
}
```

## Usage Example

```yaml
startFlow:
  do:
  - actionId: github_create_repo
  if: 
    conditions:
      - conditionId: user_check_authentication_exists
        name: user_authentication
        params: 
          authType: 'github'
      - conditionId: github_is_user_valid
        params:
          githubUserName: "${outputs.user_authentication.value.nickname}"
    then:
      ...
```

The `user_check_authentication_exists` condition is used to verify that user authenticated itself using Github.

## Relevant Triggers

All triggers
