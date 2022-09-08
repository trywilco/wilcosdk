# action_success

Category: General
Description: Check if the previously executed action block finished with success
Type: Condition

### Description

**Type**: condition

Check if previously executed action block was finished with success. It uses the `success` param set on the outputs of every named block.

## Params

- **name:** name of the action block

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: action_success
    params:
      name: newrelic_configure_with_key
  then: 
    ...
```

The `action_success` condition is used to verify that action block with the name `newrelic_configure_with_key` finished successfully

The example is taken from the `newrelic-observability` quest:

*TBD: Add link to quest*

## Relevant Triggers

All triggers
