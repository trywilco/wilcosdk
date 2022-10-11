# action_success

Category: General
Description: Check if the previously executed action block finished with success
Type: Condition

### Description

**Type**: condition

Check if a previously executed action block was finished successfully. It uses the `success` param set on the output of every named block.

## Params

- **name:** The name of the action block.

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

The `action_success` condition is used to verify that the action block with the name `newrelic_configure_with_key` finished successfully.

## Relevant Triggers

All triggers.
