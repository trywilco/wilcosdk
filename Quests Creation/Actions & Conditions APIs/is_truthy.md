# is_truthy

Category: General
Description: Test if expression is truthy
Type: Condition

### Description

**Type**: condition

Test if a given expression is true in a boolean context. Truthy expressions are expressions that not evaluates to `false`,  `null`, or `undefined`. Strings that equal to one of those are also considered non truthy. 

## Params

- **value:** the expression to be checked for truthiness

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
do:
- actionId: network_http_request
  name: call_heroku_backend
  params:
    url: "https://${user.backendHerokuAppName}.herokuapp.com/api/items?limit=10"
if:
  conditions:
  - conditionId: is_truthy
    params:
      value: ${outputs.call_heroku_backend.data?.items}
```

In this example, first we do a http request, and then check if the result is truthy. If the result is indeed truthy, it means the request was successful.

## Relevant Triggers

All triggers