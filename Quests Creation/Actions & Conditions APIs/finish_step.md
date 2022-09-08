# finish_step

Category: Quest
Description: Advance user to next step or finish quest in case this is the last step
Type: Action

## Description

**Type**: Action

Advance user to the next step in current quest, or finish quest in case this is the last step.

## Params

No params required

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:
- actionId: finish_step
```

An example from the `onboarding` quest:

[](https://github.com/trywilco/quest-onboarding/blob/main/steps/onboarding_accept_invite_generic.yml)

## Relevant Triggers

All triggers