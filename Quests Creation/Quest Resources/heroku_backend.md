# heroku_backend

Description: Heroku app hosting the backend

When specified as a resources, a fully functional Heroku app will be created for the backend and configured for the user. 

Supported properties:

- **clear:** allows clearing specific configurations from an already existing Heroku app.
    - config_vars: list of config vars to be removed.
    - buildpacks: list of buildpacks to be removed.

```yaml
resources:
- name: heroku_backend
  clear:
    config_vars:
    - NEW_RELIC_LICENSE_KEY
    - NEW_RELIC_APP_NAME
```

In this example, an Heroku app will be prepared and configured to work with the user’s app backend. If such an app exists, the keys `NEW_RELIC_LICENSE_KEY` and `NEW_RELIC_APP_NAME` will be removed.

[](https://github.com/trywilco/quest-newrelic-observability/blob/main/quest.yml)