# quest_notification

Category: Event
Description: Notify a user about an event
Type: Action

### Description

**Type**: action

Notify a user about an event that happened while playing in a quest.

## Params

- **title:** The title of the notification to be displayed. Limited to 28 characters. 
- **description**: The description to be displayed in notification. Limited to 52 characters.
- **imageUrl**: The image to be displayed in the notification. Defaults to "Hello World" image. 

## Result

A notification will show up to the user in Snack

## Usage Example

```yaml
do:
- actionId: quest_notification
  params:
    title: "quest notification title"
    description: "quest notification description"
    imageUrl: "theImageURL"
```

In this example we make a quest notification which will notify about that event while the user is playing a quest 
## Relevant Triggers

All triggers
