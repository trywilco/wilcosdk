# is_user_message_text_ready_to_continue

Category: Chat
Description: Check if user answered both with message that means they are ready to continue
Type: Condition

## Description

**Type**: Condition

In some cases the bots just want confirmation from the user that they are ready to continue. This condition verifies that text mean “ready”. Examples for relevant keywords are:

- ready
- done
- let’s go
- success

## Params

No params required. The condition uses `userMessageText` which is part of the payload sent along with the trigger when user sends message to bot

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
trigger:
  type: user_message_to_keen
  flowNode:
    if:
      conditions:
      - conditionId: is_user_message_text_ready_to_continue
      then:
        ...
```

The `is_user_message_text_ready_to_continue` condition is used to verify that the message sent by the user to `keen` means he is ready to continue.

## Relevant Triggers

- `user_message_to_<bot_name>`

## Outputs

Condition does not add additional info to `payload.outputs`
