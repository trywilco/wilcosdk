# database_check_connection_url

Category: Database
Description: Verify if database connection url is valid
Type: Condition

### Description

**Type**: condition

Verify if database connection url is valid.

## Params

- **type:** database type. One of: `mongodb` or `postgresql`. Specifying type is optional and if omitted will be equal to user’s database selection `user.database`
- **url:** Full database connection url.
    - MongoDB connection url format: `mongodb://[username:password@]host1[:port1][,...hostN[:portN]][/[defaultauthdb][?options]]`
    - PostresSQL connection url format: `postgresql://[user[:password]@][netloc][:port][/dbname][?param1=value1&...]`

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
- conditionId: database_check_connection_url
  params:
    type: '${user.database}'
    url: '${outputs.database_url_key_config.value}'
```

In this example we use the output of another condition named `database_url_key_config` to check if it is a valid database connection url. We use the database selected by the user as the database type.

## Relevant Triggers

All triggers