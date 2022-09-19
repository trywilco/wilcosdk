# text_contains_strings

Category: String
Description: Check if text contains subset of strings.
Type: Condition

## Description

**Type**: condition

Check if text contains one of possible strings.

## Params

- **text:** Input string
- **strings:** An array of items where each item is either a string or array of strings. In case the item is array of strings, all strings must be found in the text.

## Outputs

No additional info is added to the global payload outputs.

## Usage Example

```yaml
if:
  conditions:
  - conditionId: text_contains_strings
    params:
      text: "${userMessageText}"
      strings:
      - - mobile
      - - non web
      - - android
        - ios
      - - android
        - iphone
      - - android
        - mobile
      - - iphone
        - mobile
      - - ios
        - mobile
  then:
    ...
```

The `text_contains_strings` condition is used to verify that text entered by the user in Snack means mobile/ios/android.

## Relevant Triggers

All triggers
