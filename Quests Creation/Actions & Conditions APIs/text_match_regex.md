# text_match_regex

Category: String
Description: Check if text matches regex.
Type: Condition

## Description

**Type**: condition

Check if text matches a regex

## Params

- **text:** Input string
- **regex:** Regex string. Value is used as input to `RegExp` ******constructor

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
trigger:
  type: local_page_load
  flowNode:
    if:
      conditions:
      - conditionId: text_match_regex
        params:
          text: "${path}"
          regex: "^/@"
      then:
        ...
```

The `text_match_regex` condition is used to verify that `path` param found in the payload of the trigger `local_page_load` matches the regex `^/@`

The example is taken from the `docker-localsetup` quest:

[](https://github.com/trywilco/quest-docker-localsetup/blob/main/steps/setup_frontend_docker_generic.yml)

## Relevant Triggers

All triggers
