# newrelic_license_key_valid

Category: NewRelic
Description: Check if given key is a valid new relic license key.
Type: Condition

## Description

**Type**: Condition

Check if given key is a valid new relic license key.

## Params

- **key:** The config var key

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: newrelic_license_key_valid
    params:
      licenseKey: "${outputs.new_relic_license_key_config.value}"
  then:
    ...
```

The `newrelic_license_key_valid` condition is used to check the output of a block named `new_relic_license_key_config` is indeed a valid New Relic license key.

## Relevant Triggers

All triggers
