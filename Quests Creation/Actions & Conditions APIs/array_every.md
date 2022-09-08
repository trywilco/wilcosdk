# array_every

Category: Array
Description: Tests whether all elements in an array pass specified conditions
Type: Condition

### Description

**Type**: action

Test whether all elements in an array pass specified conditions. An `item` property is available in the internal conditions to access the current item in the array.

## Params

- **array:** array of elements
- **conditions:** list of conditions to apply to the array elements

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
conditions:
- conditionId: array_all
  params:
    array: ${outputs.get_users.value}
    conditions:
      - conditionId: text_match_regex
        params: 
          text: ${item.email}
          regex: @gmail.com$
then:
  ...
```

In this example, we use the result of an action called `get_users` and verify that all user’s emails use the [gmail.com](http://gmail.com) domain.

## Relevant Triggers

All triggers
