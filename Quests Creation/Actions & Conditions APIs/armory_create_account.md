# armory_create_account

Category: Quest
Description: Create a new Armory account and tenant for the user
Type: Action

## Description

**Type**: Action

Create a new Armory account and tenant for the user, it'll also create a dedicated role to manage only this tenant. If the user already exists we'll create a new user for him with "+anythink" in the email.

## Params

No params required

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:
- actionId: armory_create_account
```

## Relevant Triggers

All triggers
