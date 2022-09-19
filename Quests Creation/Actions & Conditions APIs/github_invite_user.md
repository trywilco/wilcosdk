# github_invite_user

Category: Github
Description: Invite user to collaborate on Github repo.
Type: Action

## Description

**Type**: Action

Invite user to collaborate on Github repo

## Params

- **githubUserName:** user’s Github username

## Result

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:
- actionId: github_invite_user
  params:
    githubUserName: "${outputs.user_authentication.value.nickname}"
```

The `github_invite_user` action is used to invite user to collaborate on the Github repo created for them. `githubUserName` param in this example is set from the result of previous condition named `user_authentication`. See below for the full YAML example.

## Relevant Triggers

All triggers