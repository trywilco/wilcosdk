# heroku_check_backend_config_var

Category: Heroku
Description: Check if config variable is set (exists) for the backend Heroku app.
Type: Condition

## Description

**Type**: Condition

Check if config variable is set (exists) for the backend Heroku app. If config var exists, it is set on the condition outputs.

## Params

- **key:** The config var key

## Outputs

In config var exists, its `value` is set on the conditions outputs.

It can be referenced by other blocks using `outputs.<condition_name>.value`

## Usage Example

```yaml
if:
  conditions:
  - conditionId: heroku_check_backend_config_var
    name: new_relic_license_key_config
    params:
      key: NEW_RELIC_LICENSE_KEY
  then: 
    ...
```

The `heroku_check_backend_config_var` condition is used to check that user set the `NEW_RELIC_LICENSE_KEY` config var.

## Relevant Triggers

- `heroku_release_created`
