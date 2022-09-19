# newrelic_configure_with_key

Category: NewRelic
Description: Configure user New Relic properties using given license key
Type: Action

## Description

**Type**: Action

Configure user New Relic properties using given license key.

## Params

- **newRelicKey:** New Relic license key

## Outputs

The action sets `success` and `error` on its outputs. In case a failure happened, `success` will be false and `error` will be set to one of:

- `invalid_key_format` - key does not match the format of a valid New Relic license key. Format should match the regex `(NRAK-[A**-**Z0**-**9]{27})`
- `invalid_key`- key has valid format but is declined by New Relic.

These can be accessed using:

`${outputs.<action_name>.success}`

`${outputs.<action_name>.error}`

Note that success can also be checked using the [action_success](https://www.notion.so/action_success-697fd338bd2d4297850aaea4cbaa4e07) condition

## Usage Example

```yaml
do:
- actionId: newrelic_configure_with_key
  name: newrelic_configure_with_key
  params:
    newRelicKey: "${userMessageText}"
if:
  conditions:
  - conditionId: action_success
    params:
      name: newrelic_configure_with_key
  then:
    do:
    - actionId: bot_message
      params:
        person: lucca
        messages:
        - text: 'Do you feel seen? Because you are! Good job, now let’s move on. '
          delay: 2500
    - actionId: finish_step
  else:
    switch:
      key: "${outputs.newrelic_configure_with_key.error}"
      cases:
        invalid_key_format:
          do:
          - actionId: bot_message
            params:
              person: lucca
              messages:
              - text: This isn’t an API key, so why are you bothering me with it?
                delay: 2000
        invalid_key:
          do:
          - actionId: bot_message
            params:
              person: lucca
              messages:
              - text: Looks like an API key alright, but it ain't the right one. Try
                  again.
                delay: 2000
```

The `newrelic_configure_with_key` condition is used to try and configure user’s New Relic properties. It is checked for `success` and if was not successful, the `error` set on the action outputs is used to sent the correct message to the user

## Relevant Triggers

All triggers