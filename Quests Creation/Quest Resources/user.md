# user

Description: Used to modify user configuration

This resource allows to modify information stored on the user. This is required when quest need info to exist or be removed when user starts playing the quest.

Supported properties:

- **clear:** allows clearing specific information from the user.
    - attribute: list of attributes to remove.

```yaml
resources:
- name: user
  clear:
    attribute:
    - newrelic
```

This example will remove `newrelic` information stored on the user

[](https://github.com/trywilco/quest-newrelic-observability/edit/main/quest.yml)