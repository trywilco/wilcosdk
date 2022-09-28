# quest_event

Category: Event
Description: Notify a user about an event
Type: Action

### Description

**Type**: action

Notify a user about an event that happened while playing in a quest.

## Params

- **title:** The title of the event to be displayed in the notification.
- **description**: The description to be displayed in event notification. 
- **imageUrl**: The image to be displayed in the event notification. Defaults to "Hello World" image. 

## Result

A notification will show up to the user in Snack

## Usage Example

```yaml
do:
- actionId: quest_event
  params:
    title: "quest event title"
    description: "quest event description"
```

In this example we make a quest event to a users which will notify about that event while user is playing a quest 
## Relevant Triggers

All triggers
